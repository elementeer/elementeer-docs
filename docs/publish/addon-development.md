# Build an Addon

Elementeer addons are WordPress plugins that extend the agent tool surface. They register new MCP tools, define capabilities, and add REST API endpoints — all within the Elementeer ecosystem.

## Addon Structure

A minimal addon consists of:

```
my-elementeer-addon/
├── my-elementeer-addon.php    # Plugin bootstrap
├── composer.json              # Dependencies
└── src/
    ├── Addon.php              # Addon registration class
    └── Tools/
        └── MyTool.php         # Tool implementation
```

## Registration

Register your addon with Elementeer using the `elementeer_register_addon` hook:

```php
<?php
/**
 * Plugin Name: My Elementeer Addon
 * Description: Custom tools for Elementeer
 * Version: 1.0.0
 * Requires Plugins: elementeer
 */

use Elementeer\AddonRegistry;
use MyAddon\Addon;

add_action('elementeer_register_addons', function(AddonRegistry $registry) {
    $registry->register(new Addon());
});
```

## Addon Class

Your addon class implements the `Elementeer\Contracts\Addon` interface:

```php
<?php

namespace MyAddon;

use Elementeer\Contracts\Addon as AddonContract;
use Elementeer\Registry\CapabilityRegistry;
use Elementeer\Registry\ToolRegistry;

class Addon implements AddonContract
{
    public function id(): string
    {
        return 'my-addon';
    }

    public function name(): string
    {
        return 'My Elementeer Addon';
    }

    public function version(): string
    {
        return '1.0.0';
    }

    public function registerCapabilities(CapabilityRegistry $registry): void
    {
        $registry->registerGroup('my_addon', 'My Addon')
            ->register('my_addon:read', 'Read access to my addon data')
            ->register('my_addon:write', 'Write access to my addon data');
    }

    public function registerTools(ToolRegistry $registry): void
    {
        $registry->register(new Tools\MyCustomTool());
    }
}
```

## Defining a Tool

Tools are PHP classes that return JSON Schema definitions and handle tool invocations:

```php
<?php

namespace MyAddon\Tools;

use Elementeer\Contracts\Tool;
use Elementeer\Governance\GovernanceLevel;

class MyCustomTool implements Tool
{
    public function name(): string
    {
        return 'my_addon_get_data';
    }

    public function description(): string
    {
        return 'Retrieve custom data from the WordPress site.';
    }

    public function capabilityRequired(): string
    {
        return 'my_addon:read';
    }

    public function governanceLevel(): GovernanceLevel
    {
        return GovernanceLevel::L1;
    }

    public function inputSchema(): array
    {
        return [
            'type' => 'object',
            'properties' => [
                'post_id' => [
                    'type' => 'integer',
                    'description' => 'The post ID to retrieve data for.',
                ],
            ],
            'required' => ['post_id'],
        ];
    }

    public function handle(array $input, array $context): array
    {
        $postId = $input['post_id'];
        $data = get_post_meta($postId, '_my_custom_data', true);

        return [
            'post_id' => $postId,
            'data' => $data,
        ];
    }
}
```

## Tool Discovery

When Elementeer's MCP server connects to your WordPress site, it queries the tool registry. Your addon's tools appear alongside core Elementeer tools — the agent sees them as native operations.

The MCP server auto-generates Zod schemas from your tool's `inputSchema()` definition, providing type validation before any data reaches WordPress.

## REST API Endpoints

If your tool needs dedicated REST endpoints, register them under the Elementeer namespace:

```php
add_action('rest_api_init', function() {
    register_rest_route('elementeer/v1', '/my-addon/data/(?P<id>\d+)', [
        'methods' => 'GET',
        'callback' => [MyAddonController::class, 'getData'],
        'permission_callback' => function() {
            return current_user_can('elementeer_my_addon_read');
        },
    ]);
});
```

## Capability Integration

Capabilities you register appear in the WordPress admin under **Settings → Elementeer → API Keys**. Site owners can scope keys to include or exclude your addon's capabilities:

- `my_addon:read` — allows reading your addon's data
- `my_addon:write` — allows writing your addon's data

## Governance

Specify the governance level for each tool:

| Level | When to Use |
|-------|------------|
| `L0` | Read-only operations |
| `L1` | Safe writes (create individual items) |
| `L2` | Impactful writes (bulk operations, deletions) |
| `L3` | High-risk operations (configuration changes) |

Elementeer enforces governance automatically — you don't need to implement approval logic in your tool.

## Distribution

Publish your addon as a WordPress plugin. Users install it alongside Elementeer and it auto-registers. For marketplace distribution, see the [Addon Catalog](addon-catalog.md).

## Testing

Test your addon with the MCP server in development mode:

```bash
# Run MCP server with your test site
elementeer-mcp --config ~/.elementeer/test-config.json health

# Verify your custom tools appear
elementeer-mcp list-tools | grep my_addon
```

Your tools will appear in the agent's tool list prefixed with your tool name — the JSON Schema from `inputSchema()` drives the agent's parameter validation.

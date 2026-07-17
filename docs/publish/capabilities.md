# Register Capabilities

Elementeer's capability system controls what each API key can do. When building addons, you register custom capabilities that site owners can assign to API keys — providing fine-grained access control for your tools.

## Capability Anatomy

Each capability has:

- **Key** — a namespaced identifier (e.g., `my_addon:read`)
- **Label** — human-readable name ("Read My Addon Data")
- **Group** — category for organization in the admin UI ("My Addon")
- **Description** — explains what access the capability grants

## Registering a Capability Group

Groups organize capabilities in the WordPress admin. Register groups first:

```php
use Elementeer\Registry\CapabilityRegistry;

public function registerCapabilities(CapabilityRegistry $registry): void
{
    $group = $registry->registerGroup('bookings', 'Booking Systems');

    $group->register('bookings:read', 'Read Bookings')
        ->setDescription('View appointments, availability, and booking data');

    $group->register('bookings:write', 'Manage Bookings')
        ->setDescription('Create, update, and cancel bookings');

    $group->register('bookings:delete', 'Delete Bookings')
        ->setDescription('Permanently remove bookings and appointment history');
}
```

## Capability Scoping

Capabilities support scoping strategies:

### Simple Capability

A binary on/off capability:

```php
$group->register('analytics:read', 'View Analytics');
```

### Sub-Capabilities

Granular controls within a domain:

```php
$group->register('analytics:read', 'View Analytics');
$group->register('analytics:reports:read', 'View Reports');
$group->register('analytics:reports:export', 'Export Reports');
$group->register('analytics:settings:read', 'View Analytics Settings');
$group->register('analytics:settings:write', 'Modify Analytics Settings');
```

### Post-Type Scoped Capabilities

Capabilities scoped to specific post types:

```php
$group->register('content:read:page', 'Read Pages');
$group->register('content:read:post', 'Read Posts');
$group->register('content:read:product', 'Read Products');
```

## Wildcard Registration

Register capabilities matching a wildcard pattern:

```php
$registry->registerWildcard('my_addon:*', 'Full My Addon Access')
    ->setDescription('All read and write access to my addon features');
```

Wildcard keys like `my_addon:*` grant all capabilities under the `my_addon` namespace.

## Required Capabilities

Mark capabilities as required dependencies of others:

```php
$group->register('bookings:write', 'Manage Bookings')
    ->requires('bookings:read');
```

This ensures that a key with `bookings:write` always also has `bookings:read`.

## Capability Checks in Tools

Tools declare their required capability:

```php
public function capabilityRequired(): string
{
    return 'bookings:write';
}
```

Elementeer enforces this automatically — if the API key doesn't have the required capability, the tool call is rejected before reaching your handler.

## Presets

Define recommended capability sets for common use cases:

```php
$registry->definePreset('Booking Manager', [
    'site:read',
    'bookings:read',
    'bookings:write',
    'media:read',
]);
```

Presets appear in the WordPress admin's API key creation screen as one-click selections, making it easy for site owners to scope keys correctly.

## Admin UI Integration

Registered capabilities automatically appear in:

- **API Key creation screen** — site owners select which capabilities to include
- **API Key editing screen** — modify capabilities of existing keys
- **Capability overview** — **Settings → Elementeer → Capabilities** lists all registered capabilities with their groups and descriptions

## Core Capability Groups

Elementeer ships with these built-in groups:

| Group | Capabilities |
|-------|-------------|
| `site` | `site:read`, `site:assess` |
| `templates` | `templates:read`, `templates:write`, `templates:delete`, `templates:import` |
| `pages` | `pages:read`, `pages:write`, `pages:delete` |
| `posts` | `posts:read`, `posts:write`, `posts:delete` |
| `media` | `media:read`, `media:upload`, `media:delete` |
| `navigation` | `navigation:read`, `navigation:write` |
| `global_styles` | `global_styles:read`, `global_styles:write` |
| `seo` | `seo:read`, `seo:write` |
| `performance` | `performance:flush`, `performance:report` |
| `plugins` | `plugins:read`, `plugins:activate` |
| `users` | `users:read`, `users:write` |
| `settings` | `settings:read`, `settings:write` |

Your addon's capabilities integrate alongside these core groups.

# Antigravity Setup

Connect Elementeer to Antigravity via the Model Context Protocol. Antigravity is an AI coding agent that integrates with Elementeer for autonomous Elementor site management.

## Prerequisites

- [Elementeer MCP server installed](../../install/mcp.md) (`@elementeer/mcp`)
- [Elementeer WordPress plugin installed](../../install/plugin.md) with a configured API key
- [Antigravity](https://antigravity.dev) installed

## Configuration

Antigravity connects to MCP servers through its configuration system. Add Elementeer to your Antigravity MCP configuration:

```json
{
  "mcpServers": {
    "elementeer": {
      "command": "npx",
      "args": ["-y", "@elementeer/mcp"],
      "env": {
        "ELEMENTEER_SITE_URL": "https://your-site.com",
        "ELEMENTEER_API_KEY": "elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

## Environment Variable Setup

For production use, keep API keys out of config files:

```bash
export ELEMENTEER_SITE_URL="https://your-site.com"
export ELEMENTEER_API_KEY="elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

Antigravity inherits the shell environment. The MCP server picks up these variables automatically.

## Verification

Start Antigravity and verify the Elementeer connection:

```
Run a health check on my Elementor site.
```

Antigravity should report your site's WordPress version, Elementor version, template count, API key status, and available integrations.

## Capabilities

With Antigravity connected to Elementeer, you can:

- Run site assessments with prioritized fixes
- Manage the Elementor template library (import, export, duplicate, organize)
- Create pages with Creator Mode from structural descriptions
- Configure brand colors, typography, and logo through the Brand Setup Wizard
- Build complete theme structures (header, footer, single, archive) with the Theme Builder
- Manage navigation menus, media library, and page content
- Optimize SEO across Yoast, RankMath, SEOPress, or AIOSEO
- Flush Elementor caches and run performance reports

## Configuration File Path

Antigravity MCP configuration is stored at:

```bash
~/.antigravity/mcp.json
```

or within project-level configuration. Refer to Antigravity's documentation for version-specific config locations.

## Troubleshooting

1. Verify `elementeer-mcp health` works from your terminal
2. Confirm Antigravity can read the MCP config file
3. Check for valid JSON in the configuration
4. Ensure the Node.js runtime is in Antigravity's PATH
5. Restart Antigravity after configuration changes

If the connection fails, check Antigravity's developer tools or logs for MCP server error messages. See the [agent troubleshooting guide](../troubleshooting.md) for detailed diagnostics.

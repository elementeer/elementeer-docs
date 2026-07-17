# Claude Desktop Setup

Connect Elementeer to Claude Desktop via the Model Context Protocol. Claude gets full access to Elementeer's 128+ tools through a local MCP server.

## Prerequisites

- [Elementeer MCP server installed](../../install/mcp.md) (`@elementeer/mcp`)
- [Elementeer WordPress plugin installed](../../install/plugin.md) with a configured API key
- [Claude Desktop](https://claude.ai/download) app installed

## Configuration

Edit the Claude Desktop configuration file:

=== "macOS"
    ```bash
    code ~/Library/Application\ Support/Claude/claude_desktop_config.json
    ```

=== "Windows"
    ```bash
    code %APPDATA%\Claude\claude_desktop_config.json
    ```

=== "Linux"
    ```bash
    code ~/.config/Claude/claude_desktop_config.json
    ```

Add the Elementeer MCP server configuration:

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

If you have multiple sites, reference your config file instead:

```json
{
  "mcpServers": {
    "elementeer": {
      "command": "npx",
      "args": ["-y", "@elementeer/mcp", "--config", "/Users/yourname/.elementeer/config.json"]
    }
  }
}
```

### Global Installation Alternative

If you installed the MCP server globally:

```json
{
  "mcpServers": {
    "elementeer": {
      "command": "elementeer-mcp",
      "env": {
        "ELEMENTEER_SITE_URL": "https://your-site.com",
        "ELEMENTEER_API_KEY": "elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

## Verification

1. Restart Claude Desktop
2. Look for the :hammer: tools icon — it should show available Elementeer tools
3. Ask Claude:

```
Run an Elementeer health check on my site.
```

Claude should respond with your site's WordPress version, Elementor version, template count, and API key status.

## What Claude Can Do

Once connected, Claude has access to:

- Template management (list, import, export, duplicate, create)
- Site assessment (10-category analysis with prioritized recommendations)
- Page and post CRUD
- Media library management
- SEO analysis across Yoast, RankMath, SEOPress, and AIOSEO
- Navigation menu management
- Global style read/write
- Performance optimization (cache flush, reports)
- Brand Setup Wizard
- Creator Mode page composition
- Theme Builder Wizard

With the Advanced tier: WooCommerce, AI translation, booking systems, snapshots, change queue, and more.

## Troubleshooting

If Claude doesn't show Elementeer tools after restart:

1. Check **Claude Desktop → Developer** (or Help → Developer Tools) for MCP server logs
2. Verify `elementeer-mcp health` works from your terminal
3. Ensure the JSON is valid — check for trailing commas
4. Confirm `npx` is in your system PATH
5. Check that the API key has the expected capabilities

If the MCP server fails to start, Claude will show an error in the tools panel. See the [agent troubleshooting guide](../troubleshooting.md) for detailed diagnostic steps.

# Cursor Setup

Connect Elementeer to Cursor AI via the Model Context Protocol. Cursor's agent mode gets access to Elementeer's tool suite for Elementor site management directly in your editor.

## Prerequisites

- [Elementeer MCP server installed](../../install/mcp.md) (`@elementeer/mcp`)
- [Elementeer WordPress plugin installed](../../install/plugin.md) with a configured API key
- [Cursor](https://cursor.com) installed (version 0.42+)

## Configuration

Cursor uses a JSON configuration file for MCP servers. Create or edit:

=== "macOS"
    ```bash
    code ~/.cursor/mcp.json
    ```

=== "Windows"
    ```bash
    code %USERPROFILE%\.cursor\mcp.json
    ```

=== "Linux"
    ```bash
    code ~/.cursor/mcp.json
    ```

Add Elementeer:

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

For multi-site management, use a config file:

```json
{
  "mcpServers": {
    "elementeer": {
      "command": "npx",
      "args": ["-y", "@elementeer/mcp", "--config", "~/.elementeer/config.json"]
    }
  }
}
```

## Modes

Cursor supports Elementeer in different modes:

### Agent Mode (Recommended)

In Agent mode, Cursor can autonomously call Elementeer tools, sequence operations, and handle errors. Ask:

```
Switch to Agent mode and run a full site assessment on my Elementor site.
```

### Chat Mode

In Chat mode, Cursor can suggest tool calls using Elementeer tools. You provide context and Cursor recommends which tools to use:

```
What Elementeer tools should I use to update the global brand colors and typography?
```

### Edit Mode

In Edit mode, Cursor can apply Elementeer operations to site content directly:

```
Use Elementeer to update the meta description on all service pages.
```

## Verification

1. Open Cursor and start a chat in Agent mode
2. Ask:

```
Run elementeer_mcp_health to check my site connection.
```

Cursor should return your WordPress version, Elementor version, active templates, and API key status.

## Using Elementeer Commands

In Cursor's chat or agent interface:

```
List all Elementor templates on my site, grouped by type.
```

```
Create a new page "Services" using Creator Mode with a hero, three feature sections, and a CTA.
```

```
Run an SEO audit on the homepage and fix any critical issues.
```

```
Set up the brand: primary #6A35FF, secondary #2F5BFF, Inter font for headings, 
Source Sans Pro for body.
```

## Environment Variables in Cursor

If you prefer not to embed API keys in the config file, Cursor can read environment variables from your shell. Export them before launching Cursor:

```bash
export ELEMENTEER_SITE_URL="https://your-site.com"
export ELEMENTEER_API_KEY="elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

Then reference the env vars in your Cursor config (Cursor inherits the shell environment on launch).

## Troubleshooting

If Cursor doesn't connect to Elementeer:

1. Open Cursor command palette and search for "MCP" to check server status
2. Run `elementeer-mcp health` from a terminal to verify connectivity
3. Check `~/.cursor/mcp.json` for valid JSON syntax
4. Restart Cursor after configuration changes
5. Ensure you're using Cursor 0.42 or later (MCP support was added in 0.42)

See the [agent troubleshooting guide](../troubleshooting.md) for more diagnostic steps.

# OpenCode Setup

Connect Elementeer to OpenCode via the Model Context Protocol. OpenCode is an open-source CLI agent that works with Elementeer through MCP tool integration.

## Prerequisites

- [Elementeer MCP server installed](../../install/mcp.md) (`@elementeer/mcp`)
- [Elementeer WordPress plugin installed](../../install/plugin.md) with a configured API key
- [OpenCode](https://github.com/anomalyco/opencode) installed

## Configuration

OpenCode discovers MCP servers through its configuration. Add Elementeer to your OpenCode MCP config:

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

OpenCode's MCP configuration is typically stored in its project or global configuration. Refer to OpenCode's documentation for the exact config file location for your version.

## Environment Variable Approach

For security, use environment variables instead of inline API keys:

```bash
export ELEMENTEER_SITE_URL="https://your-site.com"
export ELEMENTEER_API_KEY="elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

Then configure OpenCode to use the MCP server without embedded secrets:

```json
{
  "mcpServers": {
    "elementeer": {
      "command": "elementeer-mcp"
    }
  }
}
```

The MCP server reads `ELEMENTEER_SITE_URL` and `ELEMENTEER_API_KEY` from the environment automatically.

## Verification

Start OpenCode and check that Elementeer tools are available:

```
List all available MCP tools.
```

You should see Elementeer's 128+ tools in the tool list. Verify connectivity:

```
Run elementeer_mcp_health to check my WordPress site connection.
```

## Using Elementeer with OpenCode

OpenCode works with Elementeer like any other MCP-compatible agent:

```
Assess my Elementor site and tell me the top issues.
```

```
List all Elementor templates grouped by type.
```

```
Create a new page using Creator Mode with a hero section, features grid, and CTA.
```

```
Update the global primary color to #7B4FFF.
```

## CLI Mode

OpenCode can be used in CLI mode for scripting:

```bash
opencode --mcp-config ~/.opencode/mcp.json prompt "Run a site assessment and save the report"
```

## Multi-Site Management

Reference different sites via the OpenCode MCP config:

```json
{
  "mcpServers": {
    "elementeer-production": {
      "command": "npx",
      "args": ["-y", "@elementeer/mcp", "--site", "production"],
      "env": {
        "ELEMENTEER_SITE_URL": "https://production.example.com",
        "ELEMENTEER_API_KEY": "elem_prod_xxxxxxxxxx"
      }
    },
    "elementeer-staging": {
      "command": "npx",
      "args": ["-y", "@elementeer/mcp", "--site", "staging"],
      "env": {
        "ELEMENTEER_SITE_URL": "https://staging.example.com",
        "ELEMENTEER_API_KEY": "elem_stage_xxxxxxxxxx"
      }
    }
  }
}
```

## Troubleshooting

1. Confirm OpenCode is configured to discover your MCP servers
2. Run `elementeer-mcp health` directly to verify site connectivity
3. Check that your MCP config JSON is valid
4. Ensure the API key has the required capabilities for your operations
5. Check OpenCode's logs for MCP connection errors

See the [agent troubleshooting guide](../troubleshooting.md) for detailed diagnostic steps.

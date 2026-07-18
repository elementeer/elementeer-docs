# Quickstart

Get Elementeer running in five minutes. You'll install the WordPress plugin, generate an API key, set up the MCP server, and run your first command.

## 1. Install the WordPress Plugin

Download the latest `elementeer-plugin.zip` from [GitHub Releases](https://github.com/elementeer/elementeer-mcp/releases), upload it to your WordPress site via **Plugins → Add New → Upload Plugin**, and activate it.

```bash
# Or install from source
git clone https://github.com/elementeer/elementeer.git wp-content/plugins/elementeer
```

### Verify Installation

```bash
curl -s https://your-site.com/wp-json/elementeer/v1/site | jq .
```

You should see your WordPress version, Elementor version, and active theme.

!!! info "Full plugin install guide"
    See [WordPress Plugin Installation](../install/plugin.md) for detailed steps, permissions, and troubleshooting.

## 2. Generate an API Key

1. Go to **Settings → Elementeer** in WordPress admin
2. Click the **API Keys** tab
3. Click **Add New Key**
4. Name it (e.g., "My First Key")
5. Select the "Standard" preset capability set
6. Click **Generate Key**
7. **Copy the key immediately** — it won't be shown again

!!! tip "Capability presets"
    - **Read-Only** — safe for testing, can't modify anything
    - **Standard** — templates, pages, media, SEO, and navigation
    - **Admin** — full access including plugins and users

## 3. Install the MCP Server

```bash
npm install -g @elementeer/mcp
```

Verify the installation:

```bash
elementeer-mcp --version
# v2.2.0
```

## 4. Configure the Connection

Create `~/.elementeer/config.json`:

```json
{
  "sites": {
    "default": {
      "url": "https://your-site.com",
      "apiKey": "elem_paste_your_key_here"
    }
  }
}
```

Or use environment variables:

```bash
export ELEMENTEER_SITE_URL="https://your-site.com"
export ELEMENTEER_API_KEY="elem_your_key_here"
```

## 5. Test the Connection

```bash
elementeer-mcp health
```

A successful response shows:

```
✓ Connected to https://your-site.com (WordPress 6.7, Elementor 3.28)
✓ API key valid (capabilities: 12)
✓ REST endpoints available (elementeer/v1)
✓ Templates: 47  |  Pages: 24  |  Media: 156
```

## 6. Connect Your AI Agent

Choose your agent:

=== "Claude Desktop"
    Add to `claude_desktop_config.json`:
    ```json
    {
      "mcpServers": {
        "elementeer": {
          "command": "npx",
          "args": ["-y", "@elementeer/mcp"],
          "env": {
            "ELEMENTEER_SITE_URL": "https://your-site.com",
            "ELEMENTEER_API_KEY": "elem_your_key_here"
          }
        }
      }
    }
    ```

=== "Cursor"
    Add to `~/.cursor/mcp.json`:
    ```json
    {
      "mcpServers": {
        "elementeer": {
          "command": "npx",
          "args": ["-y", "@elementeer/mcp"],
          "env": {
            "ELEMENTEER_SITE_URL": "https://your-site.com",
            "ELEMENTEER_API_KEY": "elem_your_key_here"
          }
        }
      }
    }
    ```

=== "OpenCode"
    Add to your OpenCode MCP config:
    ```json
    {
      "mcpServers": {
        "elementeer": {
          "command": "npx",
          "args": ["-y", "@elementeer/mcp"],
          "env": {
            "ELEMENTEER_SITE_URL": "https://your-site.com",
            "ELEMENTEER_API_KEY": "elem_your_key_here"
          }
        }
      }
    }
    ```

Restart your agent after configuration.

## 7. Run Your First Command

Ask your AI agent:

```
Run a site assessment on my Elementor site.
```

The agent discovers your site's WordPress and Elementor versions, counts templates and pages, checks SEO status, analyzes performance, and returns prioritized recommendations with the exact Elementeer tools to fix each issue.

## What's Next

- **[Architecture Overview](concepts-architecture.md)** — understand how Elementeer works under the hood
- **[Template Library](guides/templates.md)** — start managing your Elementor templates
- **[Creator Mode](guides/creator-mode.md)** — build pages from section templates
- **[Brand Setup Wizard](guides/brand-setup.md)** — configure your site's visual identity in one command

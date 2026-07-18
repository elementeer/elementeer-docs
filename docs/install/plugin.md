# WordPress Plugin Installation

The Elementeer plugin for WordPress is a standard plugin that adds a secure REST API layer for agent-to-site communication. It requires Elementor (Free or Pro) and PHP 8.0+.

## Install from GitHub Releases

This is the recommended method for production sites. Each release includes a signed ZIP file.

1. Visit the [GitHub Releases page](https://github.com/elementeer/elementeer-mcp/releases)
2. Download the latest `elementeer-plugin.zip` from the v2.2.x release
3. In your WordPress admin, go to **Plugins → Add New → Upload Plugin**
4. Choose the ZIP file and click **Install Now**
5. Click **Activate**

```bash
# Alternative: download via command line
wget https://github.com/elementeer/elementeer-mcp/releases/latest/download/elementeer-plugin.zip
```

## Install from Source

For development or if you prefer to build from source, clone the repository directly:

```bash
git clone https://github.com/elementeer/elementeer.git /wp-content/plugins/elementeer
cd /wp-content/plugins/elementeer
composer install
```

Then activate from **Plugins → Installed Plugins** in WordPress admin.

## Verify Installation

After activation, verify the REST endpoints are reachable:

```bash
curl -s https://your-site.com/wp-json/elementeer/v1/site | jq .
```

You should see a JSON response with your site's WordPress version, Elementor version, and active theme information.

!!! warning "REST API must be enabled"
    Elementeer requires the WordPress REST API to be accessible. Some security plugins and
    hosting configurations may block REST access. Verify that `/wp-json/wp/v2/` returns data
    before troubleshooting Elementeer.

If you receive a `404` response, check that:

- The plugin is active under **Plugins → Installed Plugins**
- Pretty permalinks are enabled (**Settings → Permalinks → Post name**)
- No security plugin is blocking the `/wp-json/elementeer/` namespace

## Generate Your First API Key

Elementeer uses API key authentication for all agent-to-site communication. Generate your first key:

1. Go to **Settings → Elementeer** in WordPress admin
2. Click the **API Keys** tab
3. Click **Add New Key**
4. Give it a descriptive name (e.g., "Claude Desktop" or "CI Pipeline")
5. Select the capabilities this key should have. For your first key, start with the recommended presets:
    - **Read-Only** — site assessment, template listing, diagnostics
    - **Standard** — template management, page editing, global styles
    - **Admin** — full access including plugin management and user operations
6. Click **Generate Key**
7. Copy the key immediately — it will not be shown again

!!! tip "Start with Read-Only"
    For initial testing, use a Read-Only key. Once you've confirmed the connection works,
    create additional keys with the specific capabilities your workflows need. See
    [API Keys & Capabilities](../use/concepts-api-keys.md) for scoping guidance.

## Plugin Auto-Update

The plugin checks for updates by default. You can manage this under **Settings → Elementeer → General**:

- **Stable channel** (default) — receives only tagged releases
- **Beta channel** — receives release candidates for early testing
- **Off** — disables automatic update checks

## Plugin Status

The Elementeer admin page shows your plugin version, the connection status of any MCP servers that have checked in, recent operation logs, and your active API keys. Use this dashboard to monitor agent activity on your site.

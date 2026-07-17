# MCP Server Installation

The Elementeer MCP Server is a Node.js package that runs locally on your machine or in a CI/CD environment. It implements the Model Context Protocol and translates agent commands into authenticated REST API calls to your WordPress site.

## Global Installation

Install the MCP server globally with npm:

```bash
npm install -g @elementeer/mcp
```

Verify the installation:

```bash
elementeer-mcp --version
# v2.2.0
```

Check connectivity to your WordPress site:

```bash
elementeer-mcp health
# ✓ Connected to https://your-site.com (WordPress 6.7, Elementor 3.28)
# ✓ API key valid (capabilities: 12)
# ✓ REST endpoints available (elementeer/v1)
```

## npx Usage (No Installation)

If you prefer not to install globally, use npx to run the latest version each time:

```bash
npx @elementeer/mcp --version
```

This is useful for CI/CD pipelines and ephemeral environments where you don't want a persistent installation.

!!! info "npx caching"
    npx will cache the package after first use. To always get the latest version,
    use `npx @elementeer/mcp@latest`.

## Configuration

Create the configuration file at `~/.elementeer/config.json`:

```json
{
  "sites": {
    "default": {
      "url": "https://your-site.com",
      "apiKey": "elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    }
  },
  "options": {
    "timeout": 30000,
    "retries": 3,
    "logLevel": "info"
  }
}
```

The MCP server reads this file on startup. You can also configure it with environment variables:

| Variable | Description |
|----------|-------------|
| `ELEMENTEER_SITE_URL` | Your WordPress site URL (overrides config) |
| `ELEMENTEER_API_KEY` | Your Elementeer API key (overrides config) |
| `ELEMENTEER_LOG_LEVEL` | Logging verbosity: `debug`, `info`, `warn`, `error` |

## Multi-Site Configuration

Manage multiple WordPress sites from a single MCP server:

```json
{
  "sites": {
    "default": {
      "url": "https://production.example.com",
      "apiKey": "elem_prod_xxxxxxxxxx"
    },
    "staging": {
      "url": "https://staging.example.com",
      "apiKey": "elem_stage_xxxxxxxxxx"
    },
    "client-acme": {
      "url": "https://acme.example.com",
      "apiKey": "elem_acme_xxxxxxxxxx"
    }
  }
}
```

Switch sites in your agent session by referencing the site key:

```
elementeer-mcp --site staging
```

## Testing the Connection

Run a health check against your configured site:

```bash
elementeer-mcp health
```

A successful response includes:

- REST API reachability
- WordPress and Elementor version numbers
- Active plugin list
- Available templates count
- API key capability summary

```json
{
  "status": "ok",
  "wordpress": {
    "version": "6.7",
    "site_name": "My Elementor Site"
  },
  "elementor": {
    "version": "3.28.0",
    "pro": false,
    "active": true
  },
  "templates": 47,
  "api_key": {
    "valid": true,
    "capabilities": 12,
    "expires": "2027-06-01"
  }
}
```

If the health check fails, see [Troubleshooting](troubleshooting.md) for common issues and solutions.

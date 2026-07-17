# Install Elementeer

Elementeer ships in two parts: a WordPress plugin that runs on your site, and an MCP server that runs on your machine. This page covers the installation options and prerequisites.

## What you're installing

| Component | What it does | Where it runs |
|-----------|-------------|---------------|
| **Elementeer WordPress Plugin** | Exposes a REST API for site operations; bridges AI agents to Elementor and WordPress | Your WordPress site |
| **Elementeer MCP Server** | Translates MCP protocol commands into REST API calls; handles auth, validation, and response formatting | Your local machine or CI/CD server |

## Prerequisites

Before you begin, confirm your environment meets these minimum requirements:

- **WordPress site** running **PHP 8.0** or later
- **Elementor** (free or Pro) installed and active — Elementeer requires Elementor
- **Node.js 20** or later for the MCP server
- **npm** (ships with Node.js) or **npx** for package management
- An AI agent that supports the **Model Context Protocol** (Claude Desktop, Cursor, OpenCode, Antigravity, Codex CLI)

!!! info "Elementor Pro not required"
    Elementeer works with both Elementor Free and Elementor Pro. The Free tier of Elementeer
    includes 128 tools that cover template management, site assessment, global styles, SEO,
    navigation, media, and more — no Elementor Pro license needed.

## Two installation approaches

### Approach 1: Standalone WordPress plugin

Install the Elementeer plugin on each WordPress site you want to manage. This is the standard approach for production sites.

1. [Install the WordPress plugin](plugin.md) on your site
2. [Install the MCP server](mcp.md) on your machine
3. [Configure the CLI](cli.md) with your site URL and API key

### Approach 2: Embedded (for plugin developers)

If you're building a WordPress plugin or theme that uses Elementeer internally, you can embed the Elementeer plugin as a Composer dependency. This is recommended for addon developers and agencies shipping Elementeer with their own products.

```json
{
    "require": {
        "elementeer/elementeer-plugin": "^2.2"
    }
}
```

Embedded installations inherit Elementeer's REST API without requiring end users to install the plugin separately. See [Addon Development](../publish/addon-development.md) for details.

## Installation order

1. Install the **WordPress plugin** first — the MCP server needs a live WP site to connect to
2. Generate an **API key** from the WordPress admin
3. Install the **MCP server** and configure it with your site URL and key
4. Configure your **AI agent** to use the Elementeer MCP server

Continue to [WordPress Plugin](plugin.md) to begin.

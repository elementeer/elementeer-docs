# Codex CLI Setup

Connect Elementeer to Codex CLI via the Model Context Protocol. Codex is a terminal-native AI agent that integrates with Elementeer for command-line Elementor site management.

## Prerequisites

- [Elementeer MCP server installed](../../install/mcp.md) (`@elementeer/mcp`)
- [Elementeer WordPress plugin installed](../../install/plugin.md) with a configured API key
- [Codex CLI](https://github.com/openai/codex) installed

## Configuration

Codex CLI discovers MCP servers through its configuration file. Add Elementeer to your Codex MCP configuration:

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

## Environment Variable Approach

Codex CLI inherits the terminal environment. Use environment variables for API keys:

```bash
export ELEMENTEER_SITE_URL="https://your-site.com"
export ELEMENTEER_API_KEY="elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

Then configure with just the server command:

```json
{
  "mcpServers": {
    "elementeer": {
      "command": "elementeer-mcp"
    }
  }
}
```

## CLI-Native Workflow

Codex CLI is terminal-first, making it ideal for scripting and CI/CD integration:

```bash
# Run a site assessment
codex "Run an Elementeer site assessment and report the top 5 issues"

# Template management
codex "List all Elementor templates and identify unused ones"

# Brand management
codex "Update global colors: primary #6A35FF, secondary #2F5BFF"

# Cache management
codex "Flush the Elementor CSS cache"
```

## Parallel Operations

Codex CLI supports running operations in parallel via MCP tools. For example:

```
Run SEO audits on all published pages in parallel and summarize the results.
```

The agent dispatches multiple `elementeer_analyze_seo` calls concurrently and aggregates the results.

## Verification

```bash
codex "Run elementeer_mcp_health on my WordPress site"
```

Codex should return your WordPress and Elementor versions, template count, active integrations, and API key status.

## Multi-Site with Codex

Manage multiple sites by creating separate configurations:

```bash
# Production
ELEMENTEER_SITE_URL="https://production.example.com" \
ELEMENTEER_API_KEY="elem_prod_xxx" \
codex "Assess the production site"

# Staging
ELEMENTEER_SITE_URL="https://staging.example.com" \
ELEMENTEER_API_KEY="elem_stage_xxx" \
codex "List templates on staging"
```

## CI/CD Integration

Codex CLI with Elementeer is ideal for pipeline automation:

```yaml
- name: Post-Deploy Cache Flush
  run: |
    codex "Flush the Elementor CSS cache on the production site"
  env:
    ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
    ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}

- name: Site Health Check
  run: |
    codex "Run a site assessment and exit with code 1 if score is below 70"
  env:
    ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
    ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

## Troubleshooting

1. Run `elementeer-mcp health` directly to verify site connectivity
2. Check that Codex CLI can discover MCP servers (codex version must support MCP)
3. Validate your MCP configuration JSON
4. Ensure environment variables are set in the terminal where Codex runs
5. Check Codex logs for MCP server errors

See the [agent troubleshooting guide](../troubleshooting.md) and [CI/CD setup](../../integrations/cicd.md) for more detailed guidance.

# CLI Reference

The `elementeer-mcp` command provides direct access to Elementeer operations from your terminal. It's the same server that AI agents use — useful for testing, scripting, and CI/CD pipelines.

## Command Overview

```bash
elementeer-mcp [command] [options]
```

| Command | Description |
|---------|-------------|
| `health` | Test connectivity to the configured WordPress site |
| `assess` | Run a full site assessment report |
| `list-templates` | List Elementor templates on the site |
| `import-template` | Import a template from the library |
| `export-template` | Export a template for backup |
| `list-pages` | List pages with builder status |
| `flush-cache` | Clear Elementor CSS and regeneration cache |
| `--version` | Print the MCP server version |

## Global Flags

These flags apply to all commands:

| Flag | Description |
|------|-------------|
| `--config <path>` | Path to config file (default: `~/.elementeer/config.json`) |
| `--site <name>` | Site name from multi-site config (default: `default`) |
| `--verbose` | Enable debug-level logging |
| `--json` | Output raw JSON instead of formatted text |
| `--dry-run` | Simulate the operation without making changes |

## Environment Variables

All configuration can be overridden via environment variables:

```bash
# Single-site setup
export ELEMENTEER_SITE_URL="https://mysite.com"
export ELEMENTEER_API_KEY="elem_xxxxxxxxxxxxxxxx"

elementeer-mcp health
```

These take precedence over values in `config.json`. This pattern is useful for CI/CD where you want to avoid filesystem config files:

```bash
ELEMENTEER_SITE_URL="${{ secrets.WP_URL }}" \
ELEMENTEER_API_KEY="${{ secrets.ELEMENTEER_KEY }}" \
elementeer-mcp list-templates --json
```

## Multi-Site Scripting

Target different sites from the same configuration file:

```bash
# Run assessment on production
elementeer-mcp --site production assess --json > production-report.json

# List templates on client site
elementeer-mcp --site client-acme list-templates

# Health check on staging
elementeer-mcp --site staging health
```

## CI/CD Integration

Elementeer CLI is designed for pipeline use. Example GitHub Actions step:

```yaml
- name: Site Health Check
  run: |
    npx @elementeer/mcp@latest health --json
  env:
    ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
    ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}

- name: Flush Elementor Cache After Deploy
  run: |
    npx @elementeer/mcp@latest flush-cache
  env:
    ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
    ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

See [CI/CD Setup](../integrations/cicd.md) for full pipeline examples.

## Shell Completion

Generate shell completion scripts for bash, zsh, or fish:

```bash
# zsh
elementeer-mcp completion zsh > ~/.zsh/completions/_elementeer-mcp

# bash
elementeer-mcp completion bash > /etc/bash_completion.d/elementeer-mcp

# fish
elementeer-mcp completion fish > ~/.config/fish/completions/elementeer-mcp.fish
```

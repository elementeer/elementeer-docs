# Docker Testing Environment

The Elementeer project provides a Docker-based WordPress testing environment through the `elementeer-ops/wp-testing-env` repository. Use it to test Elementeer integrations locally without affecting production sites.

## Quick Start

```bash
git clone https://git.langevc.com/elementeer-ops/wp-testing-env.git
cd wp-testing-env
docker compose up -d
```

This starts:

- **WordPress** with PHP 8.0+ on port 8080
- **MySQL** 8.0 database
- **Elementor** (Free) pre-installed
- **Elementeer** plugin pre-installed

## What's Included

The testing environment ships with:

| Component | Version | Notes |
|-----------|---------|-------|
| WordPress | 6.7 | Latest stable |
| PHP | 8.2 | Meets Elementeer requirements |
| MySQL | 8.0 | Persistent storage via Docker volume |
| Elementor | 3.28 | Free version pre-installed |
| Elementeer Plugin | Latest | Auto-downloaded from GitHub releases |
| WP-CLI | Latest | For scripting and automation |

## Accessing the Environment

After starting the container:

- **WordPress admin:** `http://localhost:8080/wp-admin`
- **Default credentials:** `admin` / `admin`
- **REST API:** `http://localhost:8080/wp-json/elementeer/v1/site`

## Generating a Test API Key

```bash
# Generate an admin-capability API key using WP-CLI
docker compose exec wordpress wp elementeer generate-key \
  --name="Test Key" \
  --capabilities="*" \
  --format=json
```

Copy the key from the JSON output and store it in `~/.elementeer/test-config.json`:

```json
{
  "sites": {
    "test": {
      "url": "http://localhost:8080",
      "apiKey": "elem_test_xxxxxxxxxxxxxxxx"
    }
  }
}
```

## Testing Elementeer Against Docker

```bash
# Health check
elementeer-mcp --config ~/.elementeer/test-config.json --site test health

# Run assessment
elementeer-mcp --config ~/.elementeer/test-config.json --site test assess

# Import test templates
elementeer-mcp --config ~/.elementeer/test-config.json --site test list-templates
```

## Development Workflow

1. Start the Docker environment
2. Make changes to the Elementeer plugin code
3. Mount your development plugin directory to test live changes:

```bash
docker compose -f docker-compose.dev.yml up -d
```

The dev compose file mounts `../elementeer-plugin/` to the WordPress plugins directory so changes take effect immediately without rebuilding.

## Integration Testing

The testing environment supports automated integration tests:

```bash
# Run the full test suite
docker compose exec wordpress wp elementeer test --all

# Run specific integration family tests
docker compose exec wordpress wp elementeer test --group=templates
docker compose exec wordpress wp elementeer test --group=seo
docker compose exec wordpress wp elementeer test --group=navigation
```

## Testing with AI Agents

Connect your agent to the Docker environment for safe experimentation:

```json
{
  "mcpServers": {
    "elementeer-test": {
      "command": "npx",
      "args": ["-y", "@elementeer/mcp", "--site", "test"],
      "env": {
        "ELEMENTEER_SITE_URL": "http://localhost:8080",
        "ELEMENTEER_API_KEY": "elem_test_key_here"
      }
    }
  }
}
```

Use a wildcard API key in the test environment for unrestricted tool access during development.

## Cleaning Up

```bash
# Stop and remove containers
docker compose down

# Remove volumes (deletes all data)
docker compose down -v

# Complete reset
docker compose down -v && docker compose up -d
```

## Available Docker Compose Profiles

| Profile | Description |
|---------|-------------|
| `default` | WordPress + Elementor + Elementeer |
| `dev` | Dev mounts for plugin and MCP server source |
| `pro` | Includes `@elementeer/pro` addon |
| `woocommerce` | Includes WooCommerce with sample products |
| `voxel` | Includes Voxel with sample listings |
| `full` | All integrations enabled |

```bash
# Start with WooCommerce
docker compose --profile woocommerce up -d

# Start with all integrations
docker compose --profile full up -d
```

# Capacium Registry

Elementeer is available through the **Capacium** registry — a package manager for developer tools. Install and manage Elementeer alongside your other CLI utilities through a unified interface.

## What is Capacium?

Capacium is a registry and package manager for developer tools, CLIs, and utilities. It provides one-line installation, version management, and dependency resolution for developer toolchains.

## Installing Elementeer via Capacium

```bash
# Install Elementeer MCP server
cap install elementeer-mcp
```

Capacium handles:
- Node.js dependency resolution
- Binary linking in your PATH
- Version selection and pinning
- Updates and rollbacks

## Available Capacium Packages

| Package | Description |
|---------|-------------|
| `elementeer-mcp` | The MCP server CLI |
| `elementeer-mcp-pro` | MCP server with Advanced tier integrations |

## Version Management

```bash
# Install a specific version
cap install elementeer-mcp@2.2.0

# List available versions
cap list elementeer-mcp

# Update to latest
cap update elementeer-mcp

# Roll back to previous version
cap rollback elementeer-mcp
```

## Installing Alongside Other Tools

Capacium manages your full developer toolchain. Install Elementeer alongside compatible tools:

```bash
cap install elementeer-mcp
cap install @anthropic/claude-code
cap install @cursor/cli
```

Capacium resolves dependencies and ensures compatible versions across your toolchain.

## Configuration

After installation via Capacium, configure Elementeer as usual:

```bash
# Capacium-managed binary
elementeer-mcp --version

# Configure site connection
elementeer-mcp config init
```

Capacium-installed tools work identically to npm-installed tools — the same `~/.elementeer/config.json` configuration applies.

## CI/CD Usage

Capacium is designed for reproducible CI/CD environments:

```yaml
- name: Install Elementeer
  uses: capacium/setup@v1
  with:
    packages: elementeer-mcp@2.2.0

- name: Health Check
  run: elementeer-mcp health
  env:
    ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
    ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

## Benefits of Capacium Installation

- **Consistent installation** across team members and CI environments
- **Version pinning** for reproducible builds
- **Dependency resolution** with other Capacium packages
- **Offline installation** with a local Capacium cache
- **Audit logging** for tool version changes

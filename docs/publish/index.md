# Publish & Extend Elementeer

Elementeer is built for extensibility. The open-core architecture lets you build addons, register custom capabilities, and publish integrations that extend what AI agents can do with Elementor.

## What You Can Build

### Addons

Addons are WordPress plugins that hook into Elementeer's extension system. They can:

- **Register new MCP tools** — expose additional operations to AI agents
- **Register new capabilities** — define custom permission scopes for your tools
- **Add REST endpoints** — create new API routes under the Elementeer namespace
- **Integrate third-party plugins** — bridge any WordPress plugin to AI agents through Elementeer

### Conversion Bridges

The Conversion Bridge API lets external systems convert their formats into Elementor JSON — HTML to Elementor, design tool exports, or any structured format that maps to Elementor's widget model.

### Custom Policies

For Studio tier deployments, you can define organizational policies that govern what agents can and cannot do across your entire site portfolio.

## Extension Architecture

```
Elementeer WordPress Plugin
    │
    ├── Core REST API (elementeer/v1)
    │
    ├── Extension Registry
    │   ├── Addon Loader
    │   ├── Capability Registry
    │   └── Tool Discovery
    │
    └── Addons
        ├── @elementeer/pro (Advanced tier features)
        ├── @elementeer/voxel (Voxel integration)
        └── Your Custom Addon
```

## Getting Started

1. **[Build an Addon](addon-development.md)** — Register with Elementeer, create tools, and expose capabilities
2. **[Register Capabilities](capabilities.md)** — Define permission scopes that control tool access
3. **[Browse the Addon Catalog](addon-catalog.md)** — See available addons and what they provide
4. **[Use the Bridge API](bridge-api.md)** — Convert external formats to Elementor JSON
5. **[Roadmap](roadmap.md)** — See what's planned for future releases

## Developer Resources

- **License:** Elementeer MCP server is Apache-2.0. The WordPress plugin is GPL-2.0. Addons can use any compatible license.
- **Repository:** [github.com/elementeer/elementeer-mcp](https://github.com/elementeer/elementeer-mcp)
- **Plugin Source:** [git.langevc.com/elementeer/elementeer-plugin](https://git.langevc.com/elementeer/elementeer-plugin)
- **Issues:** [GitHub Issues](https://github.com/elementeer/elementeer-mcp/issues)

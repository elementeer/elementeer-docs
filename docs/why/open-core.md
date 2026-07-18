# Open-Core Model

Elementeer uses an open-core business model. The protocol layer is open source. Advanced features fund ongoing development. This page explains what's open, what's not, and why.

## What's Open Source

### MCP Server — Apache 2.0

The `@elementeer/mcp` npm package is licensed under Apache 2.0. You can:

- Use it for any purpose, commercial or personal
- Modify and redistribute it
- Include it in your own products
- Contribute improvements back

```bash
git clone https://github.com/elementeer/elementeer-mcp.git
```

The MCP server contains:
- The MCP protocol implementation
- Zod schema definitions for all Free-tier tools
- REST API client for WordPress communication
- CLI interface
- Multi-site configuration support

### WordPress Plugin — GPL 2.0

The core Elementeer WordPress plugin is licensed under GPL 2.0, consistent with WordPress's own license. You can:

- Install it on unlimited sites
- Modify and redistribute it (under GPL 2.0)
- Use it as a foundation for your own WordPress products
- Embed it in your commercial WordPress themes and plugins

The plugin contains:
- The REST API layer (`elementeer/v1`)
- The capability and governance system
- The addon registry and extension hooks
- Core tools for templates, pages, media, SEO, navigation, performance, global styles
- Integration detection for all 8 integration families

## What's Proprietary

### @elementeer/pro Addon

The Advanced tier addon is proprietary. It funds the ongoing development of the free tier. Pro features include:

- WooCommerce product/order/category management
- AI translation (batch translation via WPML/Polylang)
- Amelia booking integration
- Unlimited snapshots with diff comparison
- Design token export
- Change queue with approval workflow
- Critical CSS generation
- AI image generation

### Studio Tier (Future)

The Studio tier — multi-site orchestration, control plane, and policy engine — will be proprietary.

## Why Open-Core?

### For Users

- **Free delivers real value.** 128 tools for unlimited sites isn't a trial — it's a complete agent-native toolkit.
- **No lock-in.** The MCP protocol is open. The core plugin is GPL. You can fork it, extend it, or replace our server with your own implementation.
- **Inspectable security.** You can audit exactly what the plugin does on your WordPress site.

### For Developers

- **Extensible foundation.** Build addons on a GPL-licensed WordPress plugin. No royalties, no platform fees.
- **Open protocol.** Anyone can build an MCP server that implements the Elementeer tool schema — the protocol is Apache 2.0.
- **Contribution-friendly.** Bug fixes, documentation improvements, and Free-tier feature additions are welcome.

### For Sustainability

- **Pro funds Free.** Advanced tier revenue supports the team that maintains the Free tier.
- **No data monetization.** Elementeer doesn't collect, store, or sell site data. Revenue comes from the Pro addon.
- **Aligned incentives.** We succeed when Elementor site operators succeed. The Free tier drives adoption; the Advanced tier captures value from power users.

## License Summary

| Component | License | Repository |
|-----------|---------|------------|
| MCP Server (`@elementeer/mcp`) | Apache 2.0 | [github.com/elementeer/elementeer-mcp](https://github.com/elementeer/elementeer-mcp) |
| WordPress Plugin (core) | GPL 2.0 | [github.com/elementeer/elementeer](https://github.com/elementeer/elementeer) |
| @elementeer/pro addon | Proprietary | Download from elementeer.xyz |
| Documentation | CC BY 4.0 | This site |

See the [License](../legal/license.md) page for full legal text and details.

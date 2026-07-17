# Addon Catalog

Available Elementeer addons that extend the agent tool surface. All addons install as standard WordPress plugins alongside the core Elementeer plugin.

## Official Addons

### @elementeer/pro

The Advanced tier addon. Unlocks 170+ tools including WooCommerce, AI translation, booking systems, snapshots, design tokens, and the change queue.

- **Status:** Active (v2.2.0)
- **License:** Proprietary
- **Install:** Download from [elementeer.xyz/pro](https://elementeer.xyz/pro)

Capabilities added:

| Group | Capabilities |
|-------|-------------|
| `woocommerce` | `woocommerce:read`, `woocommerce:write`, `woocommerce:settings` |
| `translation` | `translation:read`, `translation:write`, `translation:batch` |
| `bookings` | `bookings:read`, `bookings:write` |
| `snapshots` | `snapshots:read`, `snapshots:restore`, `snapshots:manage` |
| `design_tokens` | `design_tokens:read`, `design_tokens:export` |
| `change_queue` | `change_queue:read`, `change_queue:approve`, `change_queue:reject` |
| `critical_css` | `critical_css:generate`, `critical_css:inject` |
| `image_gen` | `image_gen:create` |

### @elementeer/voxel

Voxel Marketplace integration. Provides listing management and marketplace operations.

- **Status:** Active (v2.2.0)
- **License:** GPL-2.0 (Free tier), Proprietary (Pro features)
- **Install:** Included in core Elementeer plugin (Free tier features); Pro features require `@elementeer/pro`

Capabilities added:

| Group | Capabilities |
|-------|-------------|
| `voxel` | `voxel:read`, `voxel:write` (Free) |
| `voxel_pro` | `voxel:orders:read`, `voxel:memberships:read`, `voxel:search:manage`, `voxel:reviews:moderate` (Pro) |

## Community Addons

Community addons are third-party extensions built on Elementeer's addon API. They follow the same registration pattern as official addons.

### Building Your Own

Use the [Addon Development](addon-development.md) guide to create custom addons. Once published, submit your addon for inclusion in this catalog by opening an issue on the [Elementeer GitHub](https://github.com/elementeer/elementeer-mcp/issues).

### Addon Guidelines

For community addons, follow these practices:

- **Namespace capabilities** under your addon's unique prefix
- **Respect governance levels** — don't mark destructive operations as L1
- **Validate inputs** — use the Zod schema system for all tool parameters
- **Document your tools** — provide clear descriptions and parameter docs
- **Test with multiple agents** — ensure compatibility with Claude, Cursor, OpenCode, Antigravity, and Codex

## Addon Compatibility

| Addon | Elementeer v2.2 | Elementor 3.28+ | PHP 8.0+ | Node 20+ |
|-------|----------------|-----------------|----------|----------|
| @elementeer/pro | ✓ | ✓ | ✓ | ✓ |
| @elementeer/voxel | ✓ | ✓ | ✓ | ✓ |

## Installing Addons

1. Download the addon ZIP from its source
2. Upload to **Plugins → Add New → Upload Plugin** in WordPress admin
3. Activate the addon
4. The addon auto-registers with Elementeer on activation
5. New capabilities appear under **Settings → Elementeer → API Keys**
6. New tools appear in the MCP server's tool list on next connection

No MCP server configuration changes are needed — the server auto-discovers addon tools when it connects to your site.

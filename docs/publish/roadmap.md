# Roadmap

Elementeer's development roadmap, from the current v2.2.0 release through planned features. This is a living document — priorities shift based on community feedback and ecosystem needs.

## Current: v2.2.0 (July 2026)

Elementeer v2.2.0 is the current stable release:

- **128 Free tools** across all 8 integration families
- **WordPress plugin** with REST API, capability system, and L0-L3 governance
- **MCP server** (`@elementeer/mcp`) with Zod validation and multi-site support
- **Agent support** for Claude Desktop, Cursor, OpenCode, Antigravity, and Codex CLI
- **Template library** — full CRUD, import/export, categories, bulk operations
- **Site assessment** — 10-category analysis with prioritized recommendations
- **Brand Setup Wizard** — colors, typography, logo, homepage in one command
- **Creator Mode** — section-type matching and page composition
- **Theme Builder Wizard** — header, footer, single, archive template creation
- **Navigation menus** — full CRUD with nested structure and location assignment
- **Media management** — upload, sideload stock images, metadata, auditing
- **SEO** — multi-plugin support (Yoast, RankMath, SEOPress, AIOSEO)
- **Performance** — Elementor CSS cache flush, DB cleanup, performance reports
- **Global styles** — Elementor Kit read/write for colors, typography, buttons, forms
- **Integration families** — WooCommerce detection, Voxel listing CRUD, booking detection, LMS detection, charity plugin detection, accessibility scanning, translation coverage

## Up Next

### v2.3.0 — Q3 2026

- **Advanced-tier WooCommerce** — full product/order/category CRUD with `@elementeer/pro`
- **Voxel Pro integration** — orders, memberships, search, reviews
- **AI translation** — batch page and template translation via WPML/Polylang with draft-only publishing
- **Amelia booking** — full appointment management
- **Snapshots system** — unlimited snapshot history, diff comparison, point-in-time rollback
- **Design tokens export** — export Elementor Kit design tokens for cross-site consistency

### v2.4.0 — Q4 2026

- **Change queue UI** — visual approval workflow in WordPress admin for L2/L3 operations
- **Critical CSS** — automated Critical CSS generation and injection
- **AI image generation** — prompt-based image creation via DALL-E/Stable Diffusion
- **Batch operations** — apply template, SEO, and style changes across multiple pages
- **Enhanced governance** — auto-approval rules, agent trust scoring, per-agent policies

## Future: Studio Tier

The Studio tier targets multi-site agencies and enterprises managing large Elementor portfolios. Timeline to be determined based on Advanced tier adoption and community demand.

### Planned Studio Features

- **Multi-site orchestration** — manage operations across dozens of Elementor sites from a single control plane
- **Control Plane** — centralized governance dashboard with capability management across all sites
- **Custom policy engine** — define organizational policies: "agents can never delete published content," "all SEO changes require review," etc.
- **Batch orchestration** — apply template updates, global style changes, or security patches across all sites simultaneously with rollback
- **Team collaboration** — shared template libraries, approval workflows, role-based access control
- **Audit dashboard** — cross-site operation history, agent activity tracking, compliance reporting

## Community-Driven

Feature requests and prioritization happen on [GitHub Issues](https://github.com/elementeer/elementeer-mcp/issues). The roadmap adapts based on:

- Community votes and feedback
- Elementor ecosystem developments
- MCP protocol evolution
- Integration partner needs

## Version Support

| Version | Status | Support End |
|---------|--------|-------------|
| v2.2.x | Current | Active development |
| v2.1.x | Maintenance | December 2026 |
| v2.0.x | End of Life | September 2026 |

## Stay Updated

- [GitHub Releases](https://github.com/elementeer/elementeer-mcp/releases) — changelog and downloads
- [Elementeer Blog](https://elementeer.xyz/blog) — feature announcements and tutorials
- [GitHub Issues](https://github.com/elementeer/elementeer-mcp/issues) — feature requests and bug reports

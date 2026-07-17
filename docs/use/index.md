# Using Elementeer

Elementeer connects AI agents to Elementor through the Model Context Protocol. This section covers the concepts, guides, integrations, and agent setup you need to work effectively.

## Core Concepts

Understand how Elementeer works under the hood:

- **[Architecture](concepts-architecture.md)** — The layered system from AI agent to Elementor, with Zod validation, capability-based auth, and governance
- **[API Keys & Capabilities](concepts-api-keys.md)** — 65 capabilities across 26 groups, key scoping, rotation, and security best practices
- **[Governance Model](concepts-governance.md)** — L0-L3 tiers from instant reads to consent-required operations, with change queue and snapshots
- **[Product Tiers](concepts-tiers.md)** — Free (128 tools), Advanced (170+), and Studio (future, 250+) feature comparison

## Quickstart

New to Elementeer? Start here:

[:octicons-arrow-right-24: Quickstart Guide](quickstart.md)

## Feature Guides

### Site Building
- **[Template Library](guides/templates.md)** — List, import, export, duplicate, and manage Elementor templates
- **[Creator Mode](guides/creator-mode.md)** — Compose pages from template sections with structural roles and content injection
- **[Theme Builder Wizard](guides/theme-builder.md)** — Create headers, footers, single, and archive templates with display conditions
- **[Brand Setup Wizard](guides/brand-setup.md)** — Configure colors, typography, logo, and homepage in one operation

### Content & Media
- **[Navigation Menus](guides/menus.md)** — Full CRUD for menus, items, and location assignments
- **[Media Management](guides/media.md)** — Upload, sideload stock images, manage metadata, audit media library

### Diagnostics & Optimization
- **[Site Assessment](guides/assessment.md)** — 10-category analysis with prioritized, prescriptive recommendations
- **[SEO Operations](guides/seo.md)** — Multi-plugin support for Yoast, RankMath, SEOPress, and AIOSEO
- **[Performance](guides/performance.md)** — Cache management, performance reports, cleanup, Critical CSS
- **[Global Styles](guides/global-styles.md)** — Read/write Elementor Kit colors, typography, buttons, forms, and custom CSS

## Integrations

Elementeer connects to the Elementor ecosystem and beyond:

| Integration | Tier | What It Covers |
|------------|------|---------------|
| [WooCommerce](integrations/woocommerce.md) | Advanced | Products, orders, categories, store settings |
| [Voxel Marketplace](integrations/voxel.md) | Free/Pro | Listings, orders, memberships, search, reviews |
| [Booking Systems](integrations/booking.md) | Free/Pro | Amelia, Simply Schedule Appointments, The Events Calendar |
| [LMS Platforms](integrations/lms.md) | Free | LearnDash, Tutor LMS — course structure and enrollment |
| [Charity Plugins](integrations/charity.md) | Free | GiveWP, Charitable — forms, donations, campaigns |
| [Accessibility](integrations/accessibility.md) | Free | WCAG scanning, auto-fix, Ally integration |
| [Translation](integrations/translation.md) | Free/Pro | WPML, Polylang — coverage analysis, AI batch translation |

## Agent Setup

Connect Elementeer to your AI agent:

- **[Claude Desktop](agents/claude.md)** — `claude_desktop_config.json` setup
- **[Cursor](agents/cursor.md)** — `~/.cursor/mcp.json` configuration
- **[OpenCode](agents/opencode.md)** — MCP server config for the open-source CLI agent
- **[Antigravity](agents/antigravity.md)** — Antigravity MCP configuration
- **[Codex CLI](agents/codex.md)** — Terminal-native setup with environment variables

## Troubleshooting

Running into issues? See the [agent troubleshooting guide](troubleshooting.md) for MCP connection problems, tool discovery failures, and governance blocks.

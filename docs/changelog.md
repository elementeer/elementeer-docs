# Changelog

All notable changes to Elementeer.

## v2.2.0 (July 2026)

### Added

- **Creator Mode** — compose Elementor pages from section templates with structural role matching. Support for precision mode (exact template IDs) and creative mode (structural match). Content injection from structured data.
- **Theme Builder Wizard** — automated creation of Elementor Theme Builder templates (header, footer, single, archive, 404) with display condition configuration. Batch theme creation for complete theme structure setup.
- **Brand Setup Wizard** — single-command brand configuration: Elementor Kit colors, typography, site logo, and homepage assignment. Post-wizard verification against brand definitions.
- **Navigation Menu CRUD** — full create, read, update, delete for menus, menu items with nested hierarchy, and menu location assignment.
- **Media Management** — upload from URL/base64/file path, stock image search and sideload (Openverse/Unsplash/Pexels/Pixabay), metadata batch updates, media audit.
- **SEO Multi-Plugin** — unified interface for Yoast, RankMath, SEOPress, and AIOSEO. Meta read/write, focus keyword management, readability analysis, cross-plugin analysis.
- **Performance Tools** — Elementor CSS cache management (flush, status), database cleanup (revisions, transients, orphans), performance reports, image optimization audit.
- **Global Styles** — read and write Elementor Kit system colors, global typography, button styles, form field styles, and global custom CSS injection.
- **Voxel Free Integration** — detect Voxel, list post types and fields, listing CRUD operations. Pro features: orders, memberships, search, reviews.
- **Booking Integration** — detect Amelia, Simply Schedule Appointments, The Events Calendar. Read services, bookings, events.
- **LMS Integration** — detect LearnDash and Tutor LMS. Course structure analysis, lesson/quiz inventory, enrollment stats.
- **Charity Integration** — detect GiveWP and Charitable. Form/campaign listing, donation stats, donor information.
- **Accessibility** — WCAG scanning (2.0, 2.1, 2.2 at A/AA), auto-fix for common violations, Ally detection.
- **Translation Integration** — detect WPML and Polylang. Translation coverage analysis, content gap reporting.
- **Agent Support** — Claude Desktop, Cursor, OpenCode, Antigravity, Codex CLI setup guides.

### Changed

- Architecture documentation updated to reflect all 8 integration families
- Governance model extended to cover new tool categories
- Product tiers page updated with complete feature comparison table
- Site assessment now covers 10 categories (was 7)

### Fixed

- Template import handling for non-standard Elementor JSON structures
- API key capability checking for nested tool calls
- MCP server reconnection behavior after WordPress plugin deactivation/reactivation

## v2.1.0 (April 2026)

### Added

- Multi-site configuration support in MCP server
- CLI `--site` flag for targeting specific sites in multi-site configs
- Environment variable configuration (`ELEMENTEER_SITE_URL`, `ELEMENTEER_API_KEY`)
- npx usage mode alongside global installation
- Docker testing environment (`elementeer-ops/wp-testing-env`)

### Changed

- MCP server now validates inputs with Zod schemas before REST API calls
- Health check response now includes template count and media count
- Rate limiting applied per governance level (L0: 120/min, L1: 60/min, L2-L3: 10/min)

### Fixed

- REST API auth header parsing for keys with special characters
- Elementor version detection on sites with custom Elementor paths

## v2.0.0 (January 2026)

### Added

- Initial public release
- WordPress plugin with REST API under `/wp-json/elementeer/v1/`
- MCP server (`@elementeer/mcp`) with 100+ free tools
- L0-L3 governance model with change queue
- API key system with 65 capabilities across 26 groups
- Site assessment (7 categories) with recommendation engine
- Template library CRUD (list, create, read, update, delete, import, export, duplicate)
- Page and post management
- WooCommerce detection
- CLI with `health`, `assess`, `list-templates`, `import-template`, `export-template`, `flush-cache` commands
- Claude Desktop MCP integration
- Elementor Pro detection

### Architecture

- MCP protocol (stdio transport) with JSON-RPC
- Zod schema validation layer
- Capability-based authentication with WordPress plugin integration
- Governance enforcement at REST API layer
- Open-core: MCP server Apache-2.0, plugin GPL-2.0

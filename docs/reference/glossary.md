# Glossary

Definitions for terms used throughout Elementeer documentation.

## A

### Addon
A WordPress plugin that extends Elementeer with additional MCP tools, capabilities, and integrations. Official addons include `@elementeer/pro` and `@elementeer/voxel`. Community addons follow the same registration pattern.

### Agent
An AI system (Claude, Cursor, OpenCode, Antigravity, Codex) that connects to Elementeer via the Model Context Protocol and invokes tools to manage Elementor sites.

### Agent-Native
Software designed from the ground up for AI agent interaction — typed tool interfaces, structured responses, and protocol-level integration rather than screen scraping or natural language APIs bolted onto legacy systems.

### API Key
A unique token generated in the WordPress admin that authenticates MCP server connections. Keys are scoped to specific capabilities and can be revoked at any time.

## B

### Brand Setup Wizard
An Elementeer feature that configures Elementor Kit colors, typography, logo, and homepage in a single multi-tool operation.

## C

### Capability
A named permission (e.g., `templates:write`) that controls whether an API key can invoke specific operations. There are 65 capabilities across 26 groups.

### Change Queue
An Advanced-tier feature that provides a review panel for L2 and L3 governance operations. Site owners approve or reject queued changes.

### Conversion Bridge API
An API that transforms external formats (HTML, URLs) into Elementor-compatible JSON for import as templates or pages.

### Creator Mode
An Elementeer feature that composes complete Elementor pages by matching structural roles to section templates and injecting content.

## E

### Elementor
The WordPress page builder that Elementeer integrates with. Elementeer requires Elementor (Free or Pro) version 3.28+.

### Elementor Kit
Elementor's global design system — system colors, typography, button styles, form styles, and custom CSS that cascade to all widgets and templates. Formerly called "Site Settings."

### Elementeer Plugin
The WordPress plugin component of Elementeer — a GPL-2.0 licensed PHP plugin that exposes the REST API, capability system, and governance model.

## G

### Governance
Elementeer's four-level safety model (L0-L3) that determines whether operations execute immediately, are queued for review, or require explicit consent.

## I

### Integration Family
A category of related operations. Elementeer covers 8 integration families: Elementor Core, WordPress CRUD, Template Management, Media Operations, SEO Tooling, Navigation Management, Performance, and Accessibility.

## L

### L0 (Read-Only)
Governance level for operations that only read data. Execute immediately with no approval.

### L1 (Safe Writes)
Governance level for low-risk write operations. Execute directly with API key capability check.

### L2 (Impactful Writes)
Governance level for operations with significant scope. Automatically queued for admin review.

### L3 (Consent-Required)
Governance level for high-risk operations. Require explicit, per-operation consent.

## M

### MCP (Model Context Protocol)
An open standard published by Anthropic for connecting AI agents to external tools and data sources. Elementeer implements MCP as its agent-facing protocol.

### MCP Server
The `@elementeer/mcp` npm package — a Node.js application that translates MCP protocol commands into authenticated REST API calls to WordPress.

## P

### Post Type
A content type in WordPress. Standard types include `post` and `page`. Elementeer supports custom post types and Elementor template types.

## R

### REST API
The WordPress plugin's HTTP API under `/wp-json/elementeer/v1/`. Every MCP tool invocation maps to one or more REST API calls.

## S

### Site Assessment
A 10-category analysis of an Elementor-powered WordPress site, producing a scored report with prioritized, prescriptive recommendations.

### Snapshot
A point-in-time record of content state, created automatically before write operations. Snapshots enable rollback and diff comparison.

### Studio Tier
The planned multi-site orchestration tier for agencies and enterprises — control plane, policy engine, and batch operations across portfolios.

## T

### Template
An Elementor design saved in the template library. Types include `page`, `section`, `header`, `footer`, `single`, `archive`, `popup`, `loop-item`, `product`, and `product-archive`.

### Theme Builder
Elementor Pro's templating system for creating site-wide headers, footers, single/archive templates, and 404 pages with display conditions.

### Tool
A typed, documented, capability-gated operation exposed through the MCP protocol. Elementeer provides 128 Free-tier tools and 250+ total.

## Z

### Zod
A TypeScript-first schema validation library used by the MCP server to validate all tool inputs before they reach WordPress. Catches type errors at the protocol boundary.

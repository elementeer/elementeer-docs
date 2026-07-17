# The Elementor Ecosystem

Elementeer is built for Elementor — not as a generic WordPress tool, but as a deep integration with Elementor's internal systems, template model, global style engine, and widget architecture.

## Why Elementor?

Elementor powers over 16 million websites. It's the dominant page builder in the WordPress ecosystem. Its market share means that operational efficiency at scale — managing templates, enforcing brand consistency, optimizing performance — directly impacts a significant portion of the web.

But Elementor's administrative surface is designed for human interaction. Click, drag, configure. This is excellent for design work, but creates friction for operations:

- **Template management:** Exporting, importing, and organizing templates across sites requires manual JSON file handling
- **Global styles:** Updating brand colors across a portfolio means opening the Kit editor on every site
- **Theme Builder:** Creating matching headers and footers with display conditions requires repetitive setup
- **SEO:** Optimizing meta across Elementor pages requires switching between the builder and SEO plugins
- **Performance:** Flushing Elementor's CSS cache requires navigating to the Elementor Tools page

## Deep Integration, Not Surface-Level

Elementeer doesn't just wrap WordPress REST endpoints. It integrates directly with:

### Elementor Template System

Elementeer reads and writes Elementor's internal template storage. It understands template types (page, section, header, footer, single, archive, popup, loop-item, product, product-archive), template status, display conditions, and the relationship between templates and the Elementor Library.

### Elementor Kit (Global Styles)

Elementeer reads and writes the Elementor Kit's system colors, global typography, button styles, form styles, and custom CSS. Changes cascade to all widgets and templates using system colors — just like editing the Kit manually, but programmatically.

### Elementor's CSS Engine

Elementeer manages Elementor's CSS cache — flushing stale files, triggering regeneration, and monitoring the cache's health. It understands the CSS print method (internal vs external file) and can recommend optimal settings.

### Elementor's Widget Model

Elementeer understands Elementor's section → column → widget hierarchy. It can read widget settings, update widget content, and validate widget configurations against Elementor's control schema.

### Elementor Experiments

Elementeer reads and manages Elementor's experimental features — Improved CSS Loading, Optimized DOM Output, Inline Font Icons, Flexbox Container, and more. It can enable performance-optimizing experiments across sites.

## Bypassing REST Limitations

Elementor's native REST API is limited:
- It exposes Elementor data through the builder's internal API, not a public contract
- It's version-dependent and subject to change
- It lacks authentication granularity

Elementeer provides a stable, versioned REST API (`/wp-json/elementeer/v1/`) that maps to Elementor's internals while maintaining backward compatibility. When Elementor's internal API changes, Elementeer absorbs the change — the agent-facing API remains stable.

## Integration Families

Elementeer covers the full Elementor ecosystem through 8 integration families:

1. **Elementor Core** — widget, template, kit, and experiment operations
2. **WordPress CRUD** — pages, posts, custom post types
3. **Template Management** — library ops, categories, tags, bulk operations
4. **Media Operations** — upload, sideload, metadata, audit
5. **SEO Tooling** — Yoast, RankMath, SEOPress, AIOSEO
6. **Navigation** — menus, items, locations
7. **Performance** — cache, reports, cleanup
8. **Accessibility** — scanning, reporting, auto-fix

Plus integrations for WooCommerce, Voxel, booking systems, LMS platforms, charity plugins, and translation — the tools you already use, made agent-native.

## Not Replacing, Augmenting

Elementeer doesn't replace Elementor's UI, the WordPress admin, or the builder workflow. It adds an operational layer — a way to interact with your Elementor site through structured, typed, agent-accessible tools while continuing to use the builder, admin, and dashboard exactly as before.

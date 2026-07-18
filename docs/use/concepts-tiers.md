# Product Tiers

Elementeer ships in three tiers. Every tier includes the full WordPress plugin and MCP server — tiers determine which tools and features are unlocked.

## Free Tier

**128 tools. Unlimited sites. No expiration.**

The Free tier is a complete agent-native toolkit for Elementor site management. It includes:

### Core Operations
- Template CRUD (list, create, read, update, delete, import, export, duplicate)
- Site assessment with 10 data categories
- Global styles read/write (Elementor Kit colors, typography)
- Page management (create, read, update, list)
- Post management

### Media & Content
- Media library management (upload, list, update alt text, delete)
- Stock image search and sideload (Openverse CC-licensed images)
- AI image generation prompt assistance

### Site Builders
- **Brand Setup Wizard** — configure colors, typography, logo, and homepage in one command
- **Creator Mode** — compose pages from the template library
- **Theme Builder Wizard** — create header, footer, single, and archive templates with display conditions
- Navigation menu CRUD with nested structure and menu location assignment

### SEO & Performance
- Multi-plugin SEO support (Yoast, RankMath, SEOPress, AIOSEO)
- Meta title/description read/write, focus keywords, readability analysis
- SEO audit and recommendations
- Elementor CSS cache flush
- Performance reporting

### All 8 Integration Families

The Free tier covers all integration families:

1. **Elementor Core** — template, widget, and kit operations
2. **WordPress CRUD** — pages, posts, custom post types
3. **Template Management** — library operations, categories, tags
4. **Media Operations** — upload, sideload, metadata
5. **SEO Tooling** — multi-plugin, analysis, meta management
6. **Navigation Management** — menus, items, locations
7. **Performance** — cache, reports, cleanup
8. **Accessibility** — WCAG scanning, reporting

Includes community integrations: Voxel Marketplace (listing CRUD), booking detection, LMS detection, charity plugin detection.

## Advanced Tier

**Everything in Free, plus operational power tools.**

The Advanced tier (`@elementeer/pro` addon) adds:

### E-Commerce & Business
- **WooCommerce** — full product CRUD, order management, category operations, store settings
- **Voxel Marketplace Pro** — orders, memberships, search, reviews, custom fields, taxonomies
- **Booking Systems** — Amelia, Simply Schedule Appointments, The Events Calendar integration

### Operational Tools
- **Snapshots** — full page/post snapshot history with diff comparison and rollback
- **Design Tokens** — export and manage design tokens across sites
- **Change Queue** — review, approve, or reject agent-queued operations
- **Batch Operations** — apply changes across multiple pages in one operation

### Content Intelligence
- **AI Translation** — batch translation of pages and templates via WPML/Polylang
- **Critical CSS** — generate and inject Critical CSS for performance optimization
- **Image AI Generation** — generate images through DALL-E/Stable Diffusion integration

## Studio Tier (Future)

**Multi-site orchestration and control plane.**

The Studio tier is on the roadmap for future releases and will include:

- **Multi-site management** — orchestrate operations across dozens of Elementor sites from a single dashboard
- **Control Plane** — centralized governance, capability management, and policy engine
- **Custom policy engine** — define organizational policies for what agents can and cannot do across your entire site portfolio
- **Batch orchestration** — apply template updates, global style changes, or security patches across all sites simultaneously
- **Team collaboration** — shared template libraries, approval workflows, and role-based access control

## Feature Comparison

| Feature | Free | Advanced | Studio |
|---------|------|----------|--------|
| Sites | Unlimited | Unlimited | Unlimited |
| Tools | 128 | 170+ | 250+ |
| Template CRUD | Full | Full | Full |
| Site Assessment | Full | Full | Full |
| Brand Setup Wizard | Full | Full | Full |
| Creator Mode | Full | Full | Full |
| Theme Builder | Full | Full | Full |
| Navigation Menus | Full | Full | Full |
| Media Library | Full | Full | Full |
| SEO Multi-Plugin | Full | Full | Full |
| Global Styles | Full | Full | Full |
| Performance Reports | Full | Full | Full |
| Snapshots | 10/post | Unlimited | Unlimited |
| WooCommerce | — | Full | Full |
| AI Translation | — | Full | Full |
| Booking Systems | — | Full | Full |
| Design Tokens | — | Full | Full |
| Change Queue | — | Full | Full |
| Critical CSS | — | Full | Full |
| Multi-Site Control | — | — | Full |
| Policy Engine | — | — | Full |
| Batch Orchestration | — | — | Full |

## Upgrading

The Advanced tier is activated by installing the `@elementeer/pro` addon plugin on your WordPress site. No changes to your MCP server configuration are needed — the server automatically discovers Pro capabilities when it connects to a site with the Pro addon active.

Studio tier licensing and availability will be announced on the [Elementeer roadmap](../publish/roadmap.md).

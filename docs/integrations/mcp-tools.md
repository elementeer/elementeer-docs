# MCP Tools

Elementeer exposes its operational surface through MCP tools — typed, validated, documented operations that AI agents can invoke. This page catalogs the tools available in the Free tier.

## Tool Naming Convention

All Elementeer MCP tools follow the pattern `elementeer_<action>_<target>`:

- `elementeer_list_templates` — list all Elementor templates
- `elementeer_assess_site` — run a site assessment
- `elementeer_update_global_colors` — update Elementor Kit colors
- `elementeer_flush_elementor_cache` — flush the Elementor CSS cache

## Core Tools (Free Tier)

### Site Operations

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_mcp_health` | _(none)_ | L0 | Test connectivity, return site info, API key status, and tool counts |
| `elementeer_assess_site` | `categories` (optional array) | L0 | Run 10-category assessment with prioritized recommendations |
| `elementeer_get_site_context` | `detail` (basic/full) | L0 | Get WordPress version, plugins, theme, Elementor status |

### Template Management

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_list_templates` | `type`, `search`, `category` | L0 | List all Elementor templates with metadata |
| `elementeer_get_template` | `id` | L0 | Get full template data and content |
| `elementeer_create_template` | `title`, `type`, `content` | L1 | Create a new Elementor template |
| `elementeer_update_template` | `id`, `title`, `categories`, `tags` | L1 | Update template metadata |
| `elementeer_delete_template` | `id` | L2 | Delete a template (queued for review) |
| `elementeer_duplicate_template` | `id`, `new_title` | L1 | Duplicate an existing template |
| `elementeer_import_template` | `source`, `title` | L1 | Import a template from library or JSON |
| `elementeer_export_template` | `id` | L0 | Export a template as Elementor JSON |
| `elementeer_bulk_templates` | `ids`, `operation` | L2 | Bulk operations (delete, categorize, status change) |

### Pages & Content

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_list_pages` | `status`, `search`, `builder` | L0 | List pages with builder detection |
| `elementeer_get_page` | `id` | L0 | Get full page data and builder content |
| `elementeer_create_page` | `title`, `content`, `template_id` | L1 | Create a new page, optionally from template |
| `elementeer_update_page` | `id`, `title`, `content`, `meta` | L1 | Update page content and metadata |
| `elementeer_delete_page` | `id` | L2 | Delete a page (queued for review) |

### Global Styles

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_get_global_styles` | _(none)_ | L0 | Read Elementor Kit colors, typography, buttons, forms |
| `elementeer_update_global_colors` | `colors` object | L1 | Update Kit system colors (primary, secondary, text, accent) |
| `elementeer_update_global_typography` | `typography` object | L1 | Update Kit typography (heading and body fonts) |
| `elementeer_update_global_css` | `css` string | L1 | Inject global custom CSS via Elementor Kit |

### Navigation Menus

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_list_menus` | _(none)_ | L0 | List all navigation menus |
| `elementeer_get_menu` | `id` | L0 | Get menu with items and hierarchy |
| `elementeer_create_menu` | `name`, `description` | L1 | Create a new navigation menu |
| `elementeer_delete_menu` | `id` | L2 | Delete a menu |
| `elementeer_list_menu_locations` | _(none)_ | L0 | List registered theme menu locations |
| `elementeer_assign_menu_location` | `location`, `menu_id` | L1 | Assign or unassign menu to theme location |
| `elementeer_add_menu_item` | `menu_id`, `title`, `url`, `parent`, `position` | L1 | Add item to menu |
| `elementeer_update_menu_item` | `item_id`, `title`, `url`, `target` | L1 | Update menu item |
| `elementeer_delete_menu_item` | `item_id` | L2 | Remove menu item |

### Media Library

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_list_media` | `search`, `page`, `per_page` | L0 | List media library files |
| `elementeer_get_media` | `id` | L0 | Get media item details |
| `elementeer_upload_media` | `file`, `filename`, `title`, `alt` | L1 | Upload file to media library |
| `elementeer_update_media` | `id`, `alt`, `title`, `caption` | L1 | Update media metadata |
| `elementeer_delete_media` | `id` | L2 | Delete media file |
| `elementeer_search_stock_images` | `query`, `license_type` | L0 | Search Openverse for CC-licensed images |
| `elementeer_sideload_image` | `url`, `title`, `alt` | L1 | Download and import stock image |

### SEO

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_detect_seo_plugin` | _(none)_ | L0 | Detect active SEO plugin (Yoast, RankMath, SEOPress, AIOSEO) |
| `elementeer_analyze_seo` | `page_id` | L0 | Comprehensive SEO analysis with scores and recommendations |
| `elementeer_read_seo_meta` | `page_id` | L0 | Read page SEO metadata |
| `elementeer_update_seo_meta` | `page_id`, `title`, `description`, `keywords` | L1 | Update page SEO metadata |
| `elementeer_analyze_readability` | `page_id` | L0 | Flesch score and readability analysis |

### Performance

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_flush_elementor_cache` | _(none)_ | L1 | Clear and regenerate Elementor CSS cache |
| `elementeer_cache_status` | _(none)_ | L0 | Report cache file count, size, and health |
| `elementeer_analyze_performance` | `page_id` | L0 | Performance metrics and recommendations |
| `elementeer_analyze_images` | _(none)_ | L0 | Image optimization audit |
| `elementeer_cleanup_database` | `targets` | L2 | Clean Elementor database entries |

### Integration Detection

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_detect_woocommerce` | _(none)_ | L0 | Detect WooCommerce installation and version |
| `elementeer_detect_voxel` | _(none)_ | L0 | Detect Voxel with post types and fields |
| `elementeer_detect_booking_systems` | _(none)_ | L0 | Detect booking plugins (Amelia, SSA, TEC) |
| `elementeer_detect_lms` | _(none)_ | L0 | Detect LMS plugins (LearnDash, Tutor LMS) |
| `elementeer_detect_charity` | _(none)_ | L0 | Detect charity plugins (GiveWP, Charitable) |
| `elementeer_detect_translation` | _(none)_ | L0 | Detect multilingual plugins (WPML, Polylang) |

### Accessibility

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_scan_accessibility` | `page_id`, `standard` | L0 | WCAG compliance scan |
| `elementeer_apply_accessibility_fixes` | `scan_id`, `rules` | L2 | Auto-fix auto-fixable violations |

### Brand & Theme

| Tool | Parameters | Governance | Description |
|------|-----------|------------|-------------|
| `elementeer_brand_setup` | `colors`, `typography`, `logo`, `homepage` | L1 | Configure brand in one operation |
| `elementeer_creator_mode` | `sections`, `content`, `precision` | L1 | Compose page from template sections |
| `elementeer_theme_builder_setup` | `templates`, `conditions` | L1 | Create Theme Builder templates |

## Advanced Tier Tools

Additional tools unlocked with `@elementeer/pro`:

- WooCommerce: `woocommerce_list_products`, `woocommerce_create_product`, `woocommerce_list_orders`, `woocommerce_update_order`
- AI Translation: `elementeer_translate_page`, `elementeer_batch_translate`
- Booking: `elementeer_list_amelia_services`, `elementeer_list_amelia_bookings`
- Snapshots: `elementeer_list_snapshots`, `elementeer_restore_snapshot`, `elementeer_diff_snapshots`
- Design Tokens: `elementeer_export_design_tokens`
- Change Queue: `elementeer_list_queued_changes`, `elementeer_approve_change`, `elementeer_reject_change`
- Critical CSS: `elementeer_generate_critical_css`

## Zod Schemas

Every tool parameter is validated with Zod schemas before reaching WordPress. Example for `elementeer_update_global_colors`:

```typescript
const UpdateGlobalColorsSchema = z.object({
  colors: z.object({
    primary: z.string().regex(/^#[0-9A-Fa-f]{6}$/).optional(),
    secondary: z.string().regex(/^#[0-9A-Fa-f]{6}$/).optional(),
    text: z.string().regex(/^#[0-9A-Fa-f]{6}$/).optional(),
    accent: z.string().regex(/^#[0-9A-Fa-f]{6}$/).optional(),
  }),
});
```

This catches type errors before the API call is made — the agent never sends invalid color codes to WordPress.

See the full [MCP Tool Reference](../reference/mcp-tools.md) for complete schemas, or [REST API Reference](rest-api.md) for the underlying WordPress endpoints.

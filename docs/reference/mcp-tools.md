# MCP Tool Reference

Every Elementeer MCP tool, its parameters, required capability, governance level, and response shape.

## Tool Listing

| Tool | Capability | Gov | Description |
|------|-----------|-----|-------------|
| `elementeer_mcp_health` | `site:read` | L0 | Connectivity test, site + API key status |
| `elementeer_assess_site` | `site:assess` | L0 | 10-category site assessment |
| `elementeer_get_site_context` | `site:read` | L0 | Full site context (WP, Elementor, plugins) |
| `elementeer_list_templates` | `templates:read` | L0 | List templates with filters |
| `elementeer_get_template` | `templates:read` | L0 | Single template with content |
| `elementeer_create_template` | `templates:write` | L1 | Create new template |
| `elementeer_update_template` | `templates:write` | L1 | Update template metadata |
| `elementeer_delete_template` | `templates:delete` | L2 | Delete template |
| `elementeer_duplicate_template` | `templates:write` | L1 | Clone existing template |
| `elementeer_import_template` | `templates:import` | L1 | Import from library or JSON |
| `elementeer_export_template` | `templates:read` | L0 | Export as JSON |
| `elementeer_bulk_templates` | `templates:write` | L2 | Bulk operations |
| `elementeer_list_pages` | `pages:read` | L0 | List pages with builder info |
| `elementeer_get_page` | `pages:read` | L0 | Single page data |
| `elementeer_create_page` | `pages:write` | L1 | Create new page |
| `elementeer_update_page` | `pages:write` | L1 | Update page content + meta |
| `elementeer_delete_page` | `pages:delete` | L2 | Delete page |
| `elementeer_get_global_styles` | `global_styles:read` | L0 | Read Kit styles |
| `elementeer_update_global_colors` | `global_styles:write` | L1 | Update Kit colors |
| `elementeer_update_global_typography` | `global_styles:write` | L1 | Update Kit typography |
| `elementeer_update_global_css` | `global_styles:write` | L1 | Inject custom CSS |
| `elementeer_list_menus` | `navigation:read` | L0 | List all menus |
| `elementeer_get_menu` | `navigation:read` | L0 | Menu with items + hierarchy |
| `elementeer_create_menu` | `navigation:write` | L1 | Create menu |
| `elementeer_delete_menu` | `navigation:write` | L2 | Delete menu |
| `elementeer_list_menu_locations` | `navigation:read` | L0 | Theme locations |
| `elementeer_assign_menu_location` | `navigation:write` | L1 | Assign menu to location |
| `elementeer_add_menu_item` | `navigation:write` | L1 | Add menu item |
| `elementeer_update_menu_item` | `navigation:write` | L1 | Update menu item |
| `elementeer_delete_menu_item` | `navigation:write` | L2 | Remove menu item |
| `elementeer_list_media` | `media:read` | L0 | List media files |
| `elementeer_get_media` | `media:read` | L0 | Media details |
| `elementeer_upload_media` | `media:upload` | L1 | Upload file |
| `elementeer_update_media` | `media:upload` | L1 | Update metadata |
| `elementeer_delete_media` | `media:delete` | L2 | Delete media |
| `elementeer_search_stock_images` | `media:read` | L0 | Search CC images |
| `elementeer_sideload_image` | `media:upload` | L1 | Import stock image |
| `elementeer_detect_seo_plugin` | `seo:read` | L0 | Detect SEO plugin |
| `elementeer_analyze_seo` | `seo:read` | L0 | SEO analysis |
| `elementeer_read_seo_meta` | `seo:read` | L0 | Read page meta |
| `elementeer_update_seo_meta` | `seo:write` | L1 | Update page meta |
| `elementeer_analyze_readability` | `seo:read` | L0 | Readability report |
| `elementeer_flush_elementor_cache` | `performance:flush` | L1 | Flush CSS cache |
| `elementeer_cache_status` | `performance:report` | L0 | Cache status |
| `elementeer_analyze_performance` | `performance:report` | L0 | Performance report |
| `elementeer_analyze_images` | `performance:report` | L0 | Image audit |
| `elementeer_cleanup_database` | `performance:flush` | L2 | DB cleanup |
| `elementeer_scan_accessibility` | `accessibility:scan` | L0 | WCAG scan |
| `elementeer_apply_accessibility_fixes` | `accessibility:fix` | L2 | Auto-fix violations |
| `elementeer_brand_setup` | Multiple | L1 | Configure brand |
| `elementeer_creator_mode` | `templates:write` | L1 | Compose page |
| `elementeer_theme_builder_setup` | `templates:write` | L1 | Theme Builder setup |
| `elementeer_detect_woocommerce` | `site:read` | L0 | Detect WooCommerce |
| `elementeer_detect_voxel` | `site:read` | L0 | Detect Voxel |
| `elementeer_detect_booking_systems` | `site:read` | L0 | Detect bookings |
| `elementeer_detect_lms` | `site:read` | L0 | Detect LMS |
| `elementeer_detect_charity` | `site:read` | L0 | Detect charity |
| `elementeer_detect_translation` | `site:read` | L0 | Detect translation |

## Advanced Tier Tools

| Tool | Tier | Capability | Gov | Description |
|------|------|-----------|-----|-------------|
| `woocommerce_list_products` | Pro | `woocommerce:read` | L0 | List products |
| `woocommerce_create_product` | Pro | `woocommerce:write` | L1 | Create product |
| `woocommerce_update_product` | Pro | `woocommerce:write` | L1 | Update product |
| `woocommerce_delete_product` | Pro | `woocommerce:write` | L2 | Delete product |
| `woocommerce_list_orders` | Pro | `woocommerce:read` | L0 | List orders |
| `woocommerce_get_order` | Pro | `woocommerce:read` | L0 | Order details |
| `woocommerce_update_order` | Pro | `woocommerce:write` | L1 | Update order |
| `woocommerce_list_categories` | Pro | `woocommerce:read` | L0 | Product categories |
| `woocommerce_get_settings` | Pro | `woocommerce:settings` | L0 | Store settings |
| `woocommerce_update_settings` | Pro | `woocommerce:settings` | L3 | Update settings |
| `elementeer_translate_page` | Pro | `translation:write` | L1 | Translate page |
| `elementeer_batch_translate` | Pro | `translation:batch` | L2 | Batch translate |
| `elementeer_list_amelia_services` | Pro | `booking:read` | L0 | Amelia services |
| `elementeer_list_amelia_bookings` | Pro | `booking:read` | L0 | Amelia bookings |
| `elementeer_list_snapshots` | Pro | `snapshots:read` | L0 | List snapshots |
| `elementeer_restore_snapshot` | Pro | `snapshots:restore` | L2 | Restore snapshot |
| `elementeer_diff_snapshots` | Pro | `snapshots:read` | L0 | Compare snapshots |
| `elementeer_export_design_tokens` | Pro | `design_tokens:export` | L0 | Export tokens |
| `elementeer_import_design_tokens` | Pro | `design_tokens:export` | L1 | Import tokens |
| `elementeer_list_queued_changes` | Pro | `change_queue:read` | L0 | List queue |
| `elementeer_approve_change` | Pro | `change_queue:approve` | L1 | Approve |
| `elementeer_reject_change` | Pro | `change_queue:reject` | L1 | Reject |
| `elementeer_generate_critical_css` | Pro | `critical_css:generate` | L1 | Gen Critical CSS |
| `elementeer_generate_image` | Pro | `image_gen:create` | L1 | Generate image |

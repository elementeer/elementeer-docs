# Capability Registry

The complete Elementeer capability registry. Every capability gates a specific operation or class of operations. API keys are scoped to subsets of these capabilities.

## Core Capabilities

### Site (`site`)

| Capability | Description |
|-----------|-------------|
| `site:read` | Read site information, WordPress version, Elementor status, plugin inventory |
| `site:assess` | Run full site assessments across all 10 categories |

### Templates (`templates`)

| Capability | Description |
|-----------|-------------|
| `templates:read` | List templates, view template content and metadata |
| `templates:write` | Create, update, duplicate templates |
| `templates:delete` | Delete templates (L2 governed) |
| `templates:import` | Import templates from library or JSON |

### Pages (`pages`)

| Capability | Description |
|-----------|-------------|
| `pages:read` | List and view pages |
| `pages:write` | Create and update pages |
| `pages:delete` | Delete pages (L2 governed) |

### Posts (`posts`)

| Capability | Description |
|-----------|-------------|
| `posts:read` | List and view posts |
| `posts:write` | Create and update posts |
| `posts:delete` | Delete posts (L2 governed) |

### Media (`media`)

| Capability | Description |
|-----------|-------------|
| `media:read` | List and view media files, search stock images |
| `media:upload` | Upload files, sideload stock images, update metadata |
| `media:delete` | Delete media files (L2 governed) |

### Global Styles (`global_styles`)

| Capability | Description |
|-----------|-------------|
| `global_styles:read` | Read Kit colors, typography, buttons, forms, custom CSS |
| `global_styles:write` | Update Kit colors, typography, buttons, forms, inject custom CSS |

### Navigation (`navigation`)

| Capability | Description |
|-----------|-------------|
| `navigation:read` | List menus, view menu items, list locations |
| `navigation:write` | Create/update menus and items, assign locations |

### SEO (`seo`)

| Capability | Description |
|-----------|-------------|
| `seo:read` | Detect SEO plugin, run analysis, read meta, readability |
| `seo:write` | Update SEO metadata |

### Performance (`performance`)

| Capability | Description |
|-----------|-------------|
| `performance:flush` | Flush Elementor CSS cache, run database cleanup |
| `performance:report` | View cache status, performance reports, image audit |

### Accessibility (`accessibility`)

| Capability | Description |
|-----------|-------------|
| `accessibility:scan` | Run WCAG accessibility scans |
| `accessibility:fix` | Apply auto-fixes to accessibility violations (L2 governed) |

### Plugins (`plugins`)

| Capability | Description |
|-----------|-------------|
| `plugins:read` | List installed plugins |
| `plugins:activate` | Activate/deactivate plugins |
| `plugins:install` | Install new plugins (L3 governed) |
| `plugins:delete` | Delete plugins (L3 governed) |

### Users (`users`)

| Capability | Description |
|-----------|-------------|
| `users:read` | List and view users |
| `users:write` | Create and update users |
| `users:delete` | Delete users (L3 governed) |

### Settings (`settings`)

| Capability | Description |
|-----------|-------------|
| `settings:read` | Read WordPress and plugin settings |
| `settings:write` | Update settings (L2 governed) |

## Advanced Tier Capabilities

Available with `@elementeer/pro`:

### WooCommerce (`woocommerce`)

| Capability | Description |
|-----------|-------------|
| `woocommerce:read` | List products, orders, categories, view details |
| `woocommerce:write` | Create/update products, update orders |
| `woocommerce:settings` | Read and update store settings (settings write is L3 governed) |

### Translation (`translation`)

| Capability | Description |
|-----------|-------------|
| `translation:read` | Read translation status and coverage |
| `translation:write` | Translate individual pages |
| `translation:batch` | Run batch translations (L2 governed) |

### Bookings (`booking`)

| Capability | Description |
|-----------|-------------|
| `booking:read` | List services, bookings, availability |
| `booking:write` | Create/update appointments and services |

### Snapshots (`snapshots`)

| Capability | Description |
|-----------|-------------|
| `snapshots:read` | List snapshots, view diffs |
| `snapshots:restore` | Restore from snapshot (L2 governed) |
| `snapshots:manage` | Configure retention policies |

### Design Tokens (`design_tokens`)

| Capability | Description |
|-----------|-------------|
| `design_tokens:read` | View exported design tokens |
| `design_tokens:export` | Export and import design tokens |

### Change Queue (`change_queue`)

| Capability | Description |
|-----------|-------------|
| `change_queue:read` | View queued changes |
| `change_queue:approve` | Approve queued changes |
| `change_queue:reject` | Reject queued changes |

### Performance Advanced (`critical_css`, `image_gen`)

| Capability | Description |
|-----------|-------------|
| `critical_css:generate` | Generate Critical CSS |
| `critical_css:inject` | Inject Critical CSS into pages |
| `image_gen:create` | Generate images via AI |

## Capability Presets

Recommended capability groupings for common use cases:

### Read-Only Audit

```
site:read, site:assess, templates:read, pages:read, posts:read,
media:read, global_styles:read, navigation:read, seo:read,
performance:report, accessibility:scan
```

### Content Manager

```
site:read, templates:read, templates:write, templates:import,
pages:read, pages:write, posts:read, posts:write,
media:read, media:upload, navigation:read, navigation:write,
seo:read, seo:write, global_styles:read, global_styles:write,
performance:flush, performance:report, accessibility:scan
```

### Administrator

```
site:read, site:assess, templates:*, pages:*, posts:*,
media:*, global_styles:*, navigation:*, seo:*,
performance:*, accessibility:*, plugins:read,
users:read, settings:read
```

### Wildcard (Development Only)

```
*
```

!!! warning
    Wildcard keys grant unrestricted access. Use only in local development and testing environments. Never deploy wildcard keys to production.

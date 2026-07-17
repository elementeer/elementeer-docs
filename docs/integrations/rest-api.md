# REST API Reference

Elementeer exposes a versioned REST API under the `/wp-json/elementeer/v1/` namespace. All MCP server operations translate into calls to these endpoints. You can also call them directly from scripts, CI/CD pipelines, or custom integrations.

## Authentication

All endpoints require an Elementeer API key passed as a Bearer token:

```bash
curl -H "Authorization: Bearer elem_your_api_key" \
  https://your-site.com/wp-json/elementeer/v1/site
```

Alternatively, pass the key as a query parameter:

```bash
curl https://your-site.com/wp-json/elementeer/v1/site?api_key=elem_your_api_key
```

## Base URL

```
https://your-site.com/wp-json/elementeer/v1
```

## Endpoints

### Site Information

```http
GET /site
```

Returns WordPress version, Elementor version, active theme, plugin inventory, and API key capability summary.

**Response:**
```json
{
  "wordpress": { "version": "6.7", "site_name": "My Site" },
  "elementor": { "version": "3.28.0", "pro": true, "active": true },
  "api_key": { "valid": true, "capabilities": ["site:read", "templates:read"] }
}
```

### Site Assessment

```http
GET /assess
GET /assess?categories=performance,seo
```

Runs a 10-category site assessment. Optionally filter by category.

**Response:**
```json
{
  "score": 72,
  "categories": {
    "performance": { "score": 45, "issues": [] },
    "seo": { "score": 65, "issues": [] }
  },
  "recommendations": []
}
```

### Templates

```http
GET /templates
GET /templates?type=section&category=hero
GET /templates/{id}
POST /templates
PUT /templates/{id}
DELETE /templates/{id}
POST /templates/duplicate
```

Template operations support all Elementor template types (`page`, `section`, `header`, `footer`, `single`, `archive`, `popup`, `loop-item`, `product`, `product-archive`).

**POST /templates body:**
```json
{
  "title": "Hero Section Light",
  "type": "section",
  "content": { /* Elementor JSON */ },
  "categories": ["hero"],
  "tags": ["light", "v2"]
}
```

### Pages

```http
GET /pages
GET /pages?status=publish&search=services
GET /pages/{id}
POST /pages
PUT /pages/{id}
DELETE /pages/{id}
```

**POST /pages body:**
```json
{
  "title": "Services",
  "content": "<p>Our services</p>",
  "status": "draft",
  "template_id": 42,
  "meta": {
    "_yoast_wpseo_title": "Services — Acme Corp"
  }
}
```

### Global Styles

```http
GET /global-styles
GET /global-styles/colors
PUT /global-styles/colors
GET /global-styles/typography
PUT /global-styles/typography
PUT /global-styles/css
```

**PUT /global-styles/colors body:**
```json
{
  "primary": "#7B4FFF",
  "secondary": "#2563EB",
  "text": "#141722",
  "accent": "#10B981"
}
```

### Navigation

```http
GET /menus
GET /menus/{id}
POST /menus
DELETE /menus/{id}
GET /menus/{id}/items
POST /menus/{id}/items
PUT /menus/items/{item_id}
DELETE /menus/items/{item_id}
GET /menu-locations
PUT /menu-locations/{location}
```

**POST /menus/{id}/items body:**
```json
{
  "title": "About Us",
  "type": "page",
  "object_id": 15,
  "parent": 0,
  "position": 3
}
```

### Media

```http
GET /media
GET /media?search=logo
GET /media/{id}
POST /media
PUT /media/{id}
DELETE /media/{id}
GET /media/stock/search?query=office
POST /media/stock/sideload
```

**POST /media body:**
```json
{
  "file": "https://example.com/image.jpg",
  "filename": "hero-banner.jpg",
  "title": "Hero Banner",
  "alt": "Team collaborating"
}
```

### SEO

```http
GET /seo/detect
GET /seo/analysis/{page_id}
GET /seo/meta/{page_id}
PUT /seo/meta/{page_id}
GET /seo/readability/{page_id}
```

**PUT /seo/meta/{page_id} body:**
```json
{
  "title": "Services — Acme Corp",
  "description": "Professional web design services",
  "focus_keyword": "web design services"
}
```

### Performance

```http
GET /performance/cache
POST /performance/cache/flush
GET /performance/analysis/{page_id}
GET /performance/images
POST /performance/cleanup
```

### Accessibility

```http
GET /accessibility/scan/{page_id}?standard=wcag21aa
POST /accessibility/fix/{scan_id}
```

### Brands & Theme

```http
POST /brand-setup
POST /creator-mode
POST /theme-builder
```

### Integration Detection

```http
GET /integrations/woocommerce
GET /integrations/voxel
GET /integrations/booking
GET /integrations/lms
GET /integrations/charity
GET /integrations/translation
```

Each returns the detection status, installed version, and available data for the respective integration.

### Advanced Tier Endpoints

These require the `@elementeer/pro` addon:

```http
# WooCommerce
GET /woocommerce/products
POST /woocommerce/products
GET /woocommerce/orders
PUT /woocommerce/orders/{id}
GET /woocommerce/categories
GET /woocommerce/settings

# Translation
POST /translation/translate
POST /translation/batch

# Booking
GET /amelia/services
GET /amelia/bookings

# Snapshots
GET /snapshots?post_id=42
POST /snapshots/{uuid}/restore
GET /snapshots/{uuid_a}/diff/{uuid_b}

# Design Tokens
GET /design-tokens/export

# Change Queue
GET /change-queue
POST /change-queue/{id}/approve
POST /change-queue/{id}/reject

# Critical CSS
POST /performance/critical-css/generate
POST /performance/critical-css/inject
```

## Error Responses

All errors follow a consistent format:

```json
{
  "code": "unauthorized",
  "message": "Invalid or expired API key",
  "status": 401
}
```

Common error codes:

| Code | HTTP Status | Meaning |
|------|------------|---------|
| `unauthorized` | 401 | Missing or invalid API key |
| `forbidden` | 403 | Key lacks required capability |
| `not_found` | 404 | Resource doesn't exist |
| `governance_blocked` | 409 | Operation queued for review (L2-L3) |
| `validation_error` | 422 | Invalid request parameters |
| `plugin_inactive` | 503 | Required plugin not active |

## Rate Limiting

The REST API applies rate limiting based on governance level:
- **L0 reads:** 120 requests per minute
- **L1 writes:** 60 requests per minute
- **L2-L3 operations:** 10 requests per minute

Rate limit headers are included in every response:
```
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 87
X-RateLimit-Reset: 1629646200
```

## API Version

The current API version is `v1`. Future versions will be introduced under `/elementeer/v2/` while maintaining backward compatibility in `v1`.

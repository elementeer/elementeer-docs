# REST API Reference

Complete reference for the Elementeer REST API (`/wp-json/elementeer/v1/`). For conceptual information and usage patterns, see the [REST API guide](../../integrations/rest-api.md).

## Authentication

All endpoints require a Bearer token or `api_key` query parameter:

```
Authorization: Bearer elem_your_api_key
```

## Endpoints

### Site

```http
GET /site
```

Returns WordPress and Elementor metadata, API key status, and tool availability.

**Capability required:** `site:read`

**Response:**
```json
{
  "wordpress": {
    "version": "6.7",
    "site_name": "My Elementor Site",
    "site_url": "https://example.com",
    "debug_mode": false,
    "permalink_structure": "/%postname%/"
  },
  "elementor": {
    "version": "3.28.0",
    "pro": true,
    "active": true,
    "css_print_method": "external_file"
  },
  "api_key": {
    "valid": true,
    "name": "Claude Desktop",
    "capabilities": ["site:read", "templates:read", "templates:write"],
    "capability_count": 12,
    "expires": "2027-06-01"
  },
  "stats": {
    "templates": 47,
    "pages": 24,
    "posts": 56,
    "media": 312
  }
}
```

### Assessment

```http
GET /assess
GET /assess?categories=performance,seo,accessibility
```

Run site assessment. Optionally filter by category names.

**Capability required:** `site:assess`

**Query parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `categories` | string | Comma-separated category names to include |

**Response:**
```json
{
  "timestamp": "2026-07-17T10:00:00Z",
  "site_url": "https://example.com",
  "score": 72,
  "categories": {
    "wordpress": { "score": 95, "issues": [] },
    "elementor": { "score": 90, "issues": [] },
    "plugins": { "score": 85, "issues": [] },
    "templates": { "score": 88, "issues": [] },
    "pages": { "score": 75, "issues": [] },
    "global_styles": { "score": 80, "issues": [] },
    "seo": { "score": 65, "issues": [] },
    "performance": { "score": 45, "issues": [] },
    "accessibility": { "score": 70, "issues": [] },
    "addons": { "score": 90, "issues": [] }
  },
  "recommendations": []
}
```

### Templates

```http
GET /templates
GET /templates?type=section&category=hero&search=dark&status=publish
GET /templates/{id}
POST /templates
PUT /templates/{id}
DELETE /templates/{id}
POST /templates/duplicate
POST /templates/bulk
```

**GET /templates query parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `type` | string | Filter by template type |
| `category` | string | Filter by category slug |
| `search` | string | Search template titles |
| `status` | string | Filter by status (publish/draft) |
| `page` | int | Page number (default 1) |
| `per_page` | int | Items per page (default 20, max 100) |

**POST /templates body:**

```json
{
  "title": "Hero Section Dark",
  "type": "section",
  "content": {},
  "status": "publish",
  "categories": ["hero"],
  "tags": ["dark", "v2"]
}
```

Template types: `page`, `section`, `header`, `footer`, `single`, `archive`, `single-page`, `product`, `product-archive`, `popup`, `loop-item`.

### Pages

```http
GET /pages
GET /pages?status=publish&search=services&builder=elementor
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
    "_yoast_wpseo_title": "Services — Acme Corp",
    "_yoast_wpseo_metadesc": "Professional services"
  },
  "seo_title": "Services — Acme Corp",
  "seo_description": "Professional services overview",
  "focus_keyword": "services"
}
```

### Global Styles

```http
GET /global-styles
GET /global-styles/colors
PUT /global-styles/colors
GET /global-styles/typography
PUT /global-styles/typography
GET /global-styles/buttons
PUT /global-styles/buttons
GET /global-styles/forms
PUT /global-styles/forms
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

Each color accepts a six-character hex value with leading `#`.

### Navigation Menus

```http
GET /menus
GET /menus/{id}
POST /menus
PUT /menus/{id}
DELETE /menus/{id}
GET /menus/{id}/items
POST /menus/{id}/items
PUT /menus/items/{item_id}
DELETE /menus/items/{item_id}
GET /menu-locations
PUT /menu-locations/{location}
```

**PUT /menu-locations/{location} body:**

```json
{
  "menu_id": 3
}
```

Pass `menu_id: 0` to unassign a menu from a location.

### Media

```http
GET /media
GET /media?search=logo&page=1&per_page=20
GET /media/{id}
POST /media
PUT /media/{id}
DELETE /media/{id}
GET /media/stock/search?query=office&license_type=commercial&page=1
POST /media/stock/sideload
```

**POST /media body:**

```json
{
  "file": "https://example.com/image.jpg",
  "filename": "hero-banner.jpg",
  "title": "Hero Banner",
  "alt": "Team collaborating in office",
  "caption": "Our team"
}
```

`file` accepts a URL (HTTPS), base64-encoded string, or local file path (CLI only).

### SEO

```http
GET /seo/detect
GET /seo/analysis/{page_id}
GET /seo/meta/{page_id}
PUT /seo/meta/{page_id}
GET /seo/readability/{page_id}
```

### Performance

```http
GET /performance/cache
POST /performance/cache/flush
GET /performance/analysis/{page_id}
GET /performance/images
POST /performance/cleanup
```

**POST /performance/cleanup body:**

```json
{
  "targets": ["elementor_revisions", "elementor_transients", "css_cache_records"]
}
```

### Accessibility

```http
GET /accessibility/scan/{page_id}
GET /accessibility/scan/{page_id}?standard=wcag2aa
POST /accessibility/fix/{scan_id}
POST /accessibility/fix/{scan_id}  (body: { "rule_ids": ["image-alt", "label"] })
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

Each returns plugin detection status, version, and available data.

### Brands & Theme

```http
POST /brand-setup
POST /creator-mode
POST /theme-builder
```

## Error Schema

```json
{
  "code": "error_code",
  "message": "Human-readable error description",
  "status": 400,
  "details": {}
}
```

## Rate Limit Headers

```
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 87
X-RateLimit-Reset: 1629646200
```

## Version

Current API version: `v1`. Base path: `/wp-json/elementeer/v1/`.

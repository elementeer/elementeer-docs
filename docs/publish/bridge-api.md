# Conversion Bridge API

The Conversion Bridge API transforms external content formats into Elementor-compatible JSON. Convert HTML, URLs, design tool exports, and structured formats into native Elementor section/column/widget structures.

## What It Converts

| Source Format | Description | Output |
|--------------|-------------|--------|
| **HTML string** | Raw HTML markup with inline styles | Elementor sections, columns, and widgets |
| **URL** | External webpage content | Elementor JSON extracted from fetched HTML |
| **Design tokens** | Style definitions (colors, typography) | Elementor kit settings |
| **Structured content** | JSON content with layout annotations | Elementor page structures |

## HTML to Elementor

Submit HTML to the Conversion Bridge:

```bash
curl -X POST https://your-site.com/wp-json/elementeer/v1/bridge/convert \
  -H "Authorization: Bearer elem_your_key" \
  -H "Content-Type: application/json" \
  -d '{
    "source_type": "html",
    "content": "<section class=\"hero\"><h1>Welcome</h1><p>This is a hero section.</p></section>",
    "options": {
      "preserve_tokens": true,
      "font_substitution": true,
      "responsive": true
    }
  }'
```

The bridge maps HTML elements to Elementor widgets:

| HTML Element | Elementor Widget |
|-------------|-----------------|
| `<section>` | Section container |
| `<div class="row">` | Inner section / column layout |
| `<h1>`–`<h6>` | Heading widget |
| `<p>` | Text Editor widget |
| `<img>` | Image widget |
| `<a>` → button styling | Button widget |
| `<ul>` / `<ol>` | Icon List widget or Text Editor |
| `<form>` | Form widget |

### Fidelity Scoring

The bridge returns a fidelity score indicating how faithfully the HTML was converted:

```json
{
  "conversion_id": "conv_abc123",
  "fidelity": {
    "score": 87,
    "layout": 92,
    "typography": 85,
    "colors": 78,
    "images": 95
  },
  "warnings": [
    "Custom font 'MyCustomFont' not available — substituted with system font",
    "Gradient background simplified to solid color (#6A35FF)"
  ],
  "elementor_json": { /* Full Elementor JSON structure */ }
}
```

### Conversion Options

| Option | Default | Description |
|--------|---------|-------------|
| `preserve_tokens` | `true` | Map defined colors to Elementor global color palette |
| `font_substitution` | `true` | Substitute unavailable fonts with closest Google Fonts match |
| `responsive` | `true` | Generate tablet and mobile breakpoint adjustments |
| `create_global_colors` | `false` | Auto-create Elementor global colors from detected palette |
| `create_global_fonts` | `false` | Auto-create Elementor global fonts from detected typography |
| `strip_inline_styles` | `false` | Remove inline styles and rely on Elementor defaults |

## URL to Elementor

Convert external webpages by URL:

```json
{
  "source_type": "url",
  "url": "https://example.com/landing-page",
  "options": {
    "responsive": true,
    "font_substitution": true
  }
}
```

The bridge fetches the URL, extracts HTML, and runs the same conversion pipeline as the HTML-to-Elementor flow.

## Using Converted Content

The converted Elementor JSON can be:

- **Injected into a page** — use `elementeer_update_page` with the converted content
- **Saved as a template** — use `elementeer_create_template` to add it to the library
- **Previewed** — use the preview endpoint to see the conversion before saving

## Conversion Pipeline

```
Source Content (HTML/URL)
    │
    ├── 1. Parse — Extract DOM structure
    ├── 2. Map — Match HTML elements to Elementor widgets
    ├── 3. Style Extract — Capture CSS rules, typography, colors
    ├── 4. Responsive — Generate breakpoint variants
    ├── 5. Tokenize — Map colors to global palette (optional)
    └── 6. Output — Generate Elementor-compatible JSON
```

## API Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/elementeer/v1/bridge/convert` | POST | Convert HTML or URL to Elementor JSON |
| `/elementeer/v1/bridge/preview/{id}` | GET | Preview a previous conversion |
| `/elementeer/v1/bridge/options` | GET | Get available conversion options |

The bridge API requires the `templates:write` capability for conversion operations and `templates:read` for previews.

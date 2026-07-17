# Brand Setup Wizard

The Brand Setup Wizard configures your Elementor site's visual identity — colors, typography, logo, and homepage structure — in a single operation. It reads a brand definition and applies it to the Elementor Kit, creating consistent design tokens that flow through every template and page.

## What It Configures

A single wizard invocation sets up:

- **Elementor Kit Global Colors** — primary, secondary, accent, text, and background colors
- **Elementor Kit Typography** — heading and body font families, sizes, weights, and line heights
- **Site Logo** — uploads and sets the custom logo (used in headers, favicons, and social sharing)
- **Homepage** — optionally sets a specific page as the site's front page

## Running the Wizard

From your AI agent:

```
Set up the brand for acmecorp.com: primary #2D5BFF, secondary #FF6B35, 
accent #10B981. Use Inter for headings and Source Sans Pro for body text. 
Upload the logo from acme-logo.png.
```

The agent orchestrates multiple Elementeer tools:

```json
{
  "brand": {
    "name": "Acme Corp",
    "colors": {
      "primary": "#2D5BFF",
      "secondary": "#FF6B35",
      "accent": "#10B981",
      "text": "#1A1A2E",
      "background": "#FFFFFF"
    },
    "typography": {
      "headings": {
        "family": "Inter",
        "weights": ["400", "600", "700"]
      },
      "body": {
        "family": "Source Sans Pro",
        "weights": ["400", "600"]
      }
    },
    "logo": {
      "url": "https://example.com/wp-content/uploads/acme-logo.png"
    },
    "homepage": {
      "title": "Acme Corp — Enterprise Solutions"
    }
  }
}
```

## Tool Sequence

The wizard sequences these tool calls:

1. `elementeer_update_global_colors` — writes all color values to the Elementor Kit
2. `elementeer_update_global_typography` — configures font families and sizes
3. `elementeer_set_site_logo` — uploads and assigns the logo image
4. `elementeer_set_homepage` — sets the front page display (optional)
5. `elementeer_flush_elementor_cache` — regenerates CSS with new design tokens

All operations happen within a single agent session. The agent handles the sequencing, validation, and error recovery.

## Color System

Elementeer writes colors to the Elementor Kit's global palette. The standard slots map to Elementor's system colors:

| Brand Role | Elementor System Color |
|-----------|----------------------|
| Primary | System Color 1 |
| Secondary | System Color 2 |
| Text | System Color 3 |
| Accent | System Color 4 |
| Background | Applied as page-level background |

!!! tip "Color consistency"
    After the wizard runs, all existing templates and pages that use Elementor's system
    colors automatically pick up the new values. Templates using custom hex colors
    are not affected — the wizard preserves intentional overrides.

## Typography System

The typography configuration writes to Elementor Kit's global typography settings:

```json
{
  "headings": {
    "h1": { "size": "3rem", "weight": 700, "line_height": "1.2" },
    "h2": { "size": "2.25rem", "weight": 600, "line_height": "1.3" },
    "h3": { "size": "1.5rem", "weight": 600, "line_height": "1.4" }
  },
  "body": {
    "size": "1rem",
    "weight": 400,
    "line_height": "1.6"
  }
}
```

Elementeer auto-generates sensible defaults for heading scales when only the font family is specified — you don't need to define every level.

## Logo Handling

The wizard can handle logo setup in several ways:

- **Upload from URL** — the agent sideloads an image from a URL into the WordPress media library
- **Use existing media** — reference an existing attachment ID
- **Generate with AI** — (Advanced tier) prompt-based logo generation via AI image tools

## Batch Brand Application

For agencies managing multiple sites, run the wizard across sites:

```
Apply the Acme Corp brand to all three client sites.
```

The agent sequentially applies the brand configuration to each site using the multi-site CLI configuration:

```bash
elementeer-mcp --site client-acme brand-setup --config brand-acme.json
elementeer-mcp --site client-beta brand-setup --config brand-acme.json
elementeer-mcp --site client-gamma brand-setup --config brand-acme.json
```

## Post-Wizard Verification

After the wizard completes, verify the results:

```
Check that the brand colors and fonts are applied correctly.
```

The agent reads back the global style values and confirms they match the brand definition. Any discrepancies are reported with specific fix actions.

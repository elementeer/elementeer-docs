# Global Styles

Elementeer reads and writes Elementor's Kit-level global styles — colors, typography, buttons, form fields, and custom CSS. Your AI agent can manage design systems, enforce brand consistency, and configure light/dark mode across your entire site.

## What Are Global Styles?

Elementor's **Site Settings** (Kit) defines design tokens that cascade to every widget and template:

- **System Colors** — Primary, Secondary, Text, Accent (4 standard colors + optional custom colors)
- **Typography** — Heading and body font families, sizes, weights, and line heights
- **Buttons** — Default button padding, border radius, typography
- **Form Fields** — Input border, focus state, typography
- **Background** — Site-wide default background
- **Custom CSS** — Global CSS injected into every page

## Reading Global Colors

```
What are my current Elementor global colors?
```

The agent calls `elementeer_get_global_styles` which returns:

```json
{
  "colors": {
    "primary": "#6A35FF",
    "secondary": "#2F5BFF",
    "text": "#141722",
    "accent": "#10B981",
    "custom_colors": {
      "warning": "#F59E0B",
      "info": "#3B82F6",
      "success": "#10B981"
    }
  },
  "typography": {
    "headings": {
      "family": "Inter",
      "h1": { "size": "3rem", "weight": "700" },
      "h2": { "size": "2.25rem", "weight": "600" },
      "h3": { "size": "1.5rem", "weight": "600" }
    },
    "body": {
      "family": "Inter",
      "size": "1rem",
      "weight": "400",
      "line_height": "1.6"
    }
  },
  "buttons": {
    "padding": { "top": "12", "right": "24", "bottom": "12", "left": "24" },
    "border_radius": "4",
    "typography": { "family": "Inter", "weight": "600" }
  }
}
```

## Writing Global Colors

```
Change the primary color to #7B4FFF and the secondary to #2563EB.
```

The agent calls `elementeer_update_global_colors`:

```json
{
  "colors": {
    "primary": "#7B4FFF",
    "secondary": "#2563EB"
  }
}
```

The change is applied to the Elementor Kit and takes effect immediately. Every widget and template using System Color 1 (Primary) or System Color 2 (Secondary) will reflect the new values.

!!! tip "Cascade effect"
    Updating a global color affects all templates and pages that reference it as a
    system color. Widgets using custom hex values (not system colors) are not
    affected — global style changes are safe and predictable.

## Typography Management

```
Set Inter as the heading font and Source Sans Pro as the body font across the entire site.
```

```json
{
  "typography": {
    "headings": { "family": "Inter" },
    "body": { "family": "Source Sans Pro" }
  }
}
```

The agent can configure:

- Font family, size, weight, style, decoration
- Line height and letter spacing
- Word spacing
- Text transform (uppercase, capitalize)

## Button and Form Styles

```
Set default button border radius to 8px and use Inter Bold for button text.
```

```json
{
  "buttons": {
    "border_radius": "8",
    "typography": { "family": "Inter", "weight": "700" }
  },
  "forms": {
    "border_width": "1",
    "border_color": "#DCE2EC",
    "focus_border_color": "#6A35FF"
  }
}
```

## Global CSS Injection

```
Add global custom CSS that sets the selection color to brand purple.
```

The agent calls `elementeer_update_global_css`:

```css
::selection {
  background-color: #6A35FF;
  color: #FFFFFF;
}

::moz-selection {
  background-color: #6A35FF;
  color: #FFFFFF;
}
```

Global CSS is injected into every page via the Elementor Kit. Use it for:
- Custom selection styles
- Scrollbar styling
- Animation keyframes
- Site-wide utility classes

## Dark/Light Mode Configuration

Elementeer supports configuring color schemes for dark and light modes through Elementor's theme style system:

```
Configure a dark mode with dark backgrounds (#141722) and light text (#EEF2F8).
```

```json
{
  "schemes": {
    "light": {
      "background": "#FFFFFF",
      "text": "#141722"
    },
    "dark": {
      "background": "#141722",
      "text": "#EEF2F8"
    }
  }
}
```

## Brand Consistency Enforcement

For agencies managing multiple sites, ensure design consistency:

```
Check if all my sites are using the correct brand colors and typography.
```

The agent reads global styles from each site and compares against a brand definition:

```json
{
  "site": "client-acme",
  "drift": {
    "primary_color": "expected #6A35FF, found #6B36FF (close match)",
    "heading_font": "expected Inter, found Roboto (mismatch)"
  }
}
```

Use the [Brand Setup Wizard](brand-setup.md) to fix inconsistencies in a single operation.

## Snapshot Before Changes

Global style changes affect the entire site. Elementeer automatically creates a snapshot before applying changes so you can roll back if needed:

```
Revert to the global styles from before today's changes.
```

The snapshot captures the complete Kit state — colors, typography, buttons, forms, and custom CSS — allowing full rollback.

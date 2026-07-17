# Theme Builder Wizard

The Theme Builder Wizard automates creation of Elementor Theme Builder templates — headers, footers, single post layouts, and archive pages — with proper display conditions. A single command can create a complete set of theme templates.

## What the Wizard Creates

Elementor's Theme Builder lets you design site-wide templates that apply automatically to specific parts of your site. The wizard creates these with display conditions:

| Template | Typical Condition | What It Controls |
|----------|------------------|-----------------|
| **Header** | Entire Site | Site header with logo, navigation, CTA |
| **Footer** | Entire Site | Site footer with copyright, links, widgets |
| **Single Post** | All Posts | Blog post layout |
| **Single Page** | All Pages | Default page layout |
| **Archive** | All Archives | Category, tag, and archive listing layout |
| **Search Results** | Search Results | Search results page layout |
| **404 Page** | 404 Page | Not-found page layout |
| **Single Product** | Products | WooCommerce product detail layout |
| **Products Archive** | Product Archives | WooCommerce shop/listing layout |

## Running the Wizard

From your AI agent:

```
Set up a complete theme: header with the site logo and main menu, footer with 
copyright and social links, single post template with featured image and sidebar, 
and an archive template with a grid layout.
```

The agent:

1. Checks the Elementeer template library for matching theme templates
2. Creates each template via `elementeer_create_template` with the appropriate type
3. Sets display conditions for each template
4. Optionally imports template content from the library

## Display Conditions

Display conditions determine where a Theme Builder template appears. The wizard configures them automatically:

```
Create a header template that displays on all pages except the landing page.
```

Display condition types:

| Condition | Usage |
|-----------|-------|
| `include` | Template is active on matching locations |
| `exclude` | Template is suppressed on matching locations |
| `entire_site` | Applies everywhere |
| `singular` | Applies to single posts/pages |
| `archive` | Applies to archive/category pages |
| `by_post_type` | Applies to a specific post type |
| `by_category` | Applies to a specific category |
| `by_tag` | Applies to a specific tag |
| `by_page` | Applies to a specific page (include or exclude) |
| `search` | Applies to search results |
| `404` | Applies to 404 pages |

## Batch Theme Creation

Create all theme templates in a single session:

```
Build the entire theme: header, footer, single, archive, and 404 page.
Use dark-themed templates from the library.
```

The agent runs the full sequence:

```
1. elementeer_create_template (header, type: header, condition: entire_site)
2. elementeer_create_template (footer, type: footer, condition: entire_site)
3. elementeer_create_template (single post, type: single, condition: all posts)
4. elementeer_create_template (archive, type: archive, condition: all archives)
5. elementeer_create_template (404, type: single-page, condition: 404)
```

## Template Content Sources

The wizard can populate templates from several sources:

### From Library

The agent pulls matching templates from the Elementeer library based on template type and structural requirements.

### From Existing Templates

Clone an existing template as the basis for a Theme Builder template:

```
Create a header template using the existing "Header V3" as the base.
```

### From Description

The agent can use Creator Mode logic to assemble a theme template from sections:

```
Build a header with a centered logo, horizontal navigation, and a CTA button on the right.
```

## Post-Creation Verification

After the wizard runs, verify the theme is functioning correctly:

```
Check that all theme templates have correct display conditions and that 
the header and footer appear on the homepage.
```

The agent:

1. Lists all templates with type `header`, `footer`, `single`, and `archive`
2. Validates display conditions for each
3. Checks that the site renders correctly by fetching the homepage

## Working with Existing Theme Templates

Beyond creation, the agent can manage existing Theme Builder templates:

```
List all my Theme Builder templates with their display conditions.
```

```
Update the header template's display condition to exclude the checkout page.
```

```
Duplicate the single post template and modify the duplicated version for a custom post type.
```

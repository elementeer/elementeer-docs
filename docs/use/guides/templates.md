# Template Library

Elementeer gives your AI agent full control over the Elementor template library — list, import, export, duplicate, rename, and manage templates with typed, validated operations.

## Template Types

Elementor organizes templates into types. Elementeer supports all of them:

| Type | Description | Usage |
|------|-------------|-------|
| `page` | Full page layouts | Complete page designs |
| `section` | Reusable section patterns | Composable page building blocks |
| `header` | Site header templates | Theme Builder headers |
| `footer` | Site footer templates | Theme Builder footers |
| `single` | Single post templates | Theme Builder single post layout |
| `archive` | Archive/category templates | Theme Builder archive listing layout |
| `single-page` | Single page templates | Theme Builder single page layout |
| `product` | WooCommerce product templates | Product detail layouts |
| `product-archive` | WooCommerce shop templates | Shop/archive layouts |
| `popup` | Popup templates | Popup modals and overlays |
| `loop-item` | Loop item templates | Post/meta loop card layouts |

## Listing Templates

Ask your agent to list all templates on your site:

```
List all Elementor templates on this site, grouped by type.
```

The agent calls the `elementeer_list_templates` tool which returns type, title, status, and metadata for every template:

```json
{
  "templates": [
    {
      "id": 123,
      "title": "Hero Section Dark",
      "type": "section",
      "status": "publish",
      "categories": ["hero", "dark"],
      "modified": "2026-07-15T10:30:00Z"
    },
    {
      "id": 124,
      "title": "Homepage V2",
      "type": "page",
      "status": "publish",
      "categories": ["homepage"],
      "modified": "2026-07-14T08:15:00Z"
    }
  ],
  "total": 47,
  "by_type": {
    "page": 12,
    "section": 18,
    "header": 3,
    "footer": 3,
    "single": 5,
    "archive": 3,
    "popup": 3
  }
}
```

## Importing Templates

Elementeer can import templates from the library directly onto your site:

```
Import the "CTA Section Dark" template to this site.
```

The import operation:

1. Fetches the template JSON from the Elementeer template library
2. Validates compatibility with your Elementor version
3. Creates the template with all widget settings intact
4. Assigns categories and tags

!!! info "Template sources"
    The Free tier includes access to the Elementeer public template library. Templates
    are Elementor-native JSON — they work with any Elementor installation. No Elementor
    Pro required.

## Exporting Templates

Export any existing template for backup or transfer:

```
Export template ID 123 and save it locally.
```

The export produces Elementor-compatible JSON that can be reimported on any Elementor site:

```json
{
  "id": 123,
  "title": "Hero Section Dark",
  "type": "section",
  "content": "[Elementor JSON data]",
  "version": "3.28.0"
}
```

## Duplicating and Renaming

Create variations of existing templates without starting from scratch:

```
Duplicate the "Hero Section Dark" template and rename it to "Hero Section Light".
```

The agent calls `elementeer_duplicate_template` with the source template ID and new name. The duplicate is a complete, independent copy.

## Categories and Tags

Templates can be organized with categories and tags for easier discovery:

```
Tag all header templates with "v2-design" and move them to the "2026 Refresh" category.
```

Template metadata operations:

| Operation | Tool | Description |
|-----------|------|-------------|
| List categories | `elementeer_list_template_categories` | All template categories with counts |
| Create category | `elementeer_create_template_category` | New category with optional parent |
| Assign category | `elementeer_update_template` | Update template categories |
| Bulk tag | `elementeer_bulk_update_templates` | Apply tags across multiple templates |

## Bulk Operations

Apply operations across multiple templates in a single call:

```
Delete all templates in the "archived" category.
```

Bulk operations include:

- **Bulk delete** — remove multiple templates by ID, type, or category
- **Bulk export** — export a selection of templates as a single backup archive
- **Bulk categorize** — reassign categories across templates
- **Bulk status change** — publish or draft multiple templates

!!! warning "Bulk deletes use governance L2"
    Bulk template deletions are queued for review by default. The site owner must
    approve the operation before templates are removed. See [Governance](../concepts-governance.md).

## Template Library Stats

Get an overview of your template library:

```
How many templates do I have and what types are they?
```

The agent provides a summary including counts by type, recently modified templates, and unused templates (templates not applied to any page).

## CLI Operations

For scripting and CI/CD:

```bash
# List all templates
elementeer-mcp list-templates

# Export a specific template
elementeer-mcp export-template --id 123 > hero-dark.json

# Import from a file
elementeer-mcp import-template hero-dark.json
```

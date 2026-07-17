# Navigation Menus

Elementeer provides full CRUD operations for WordPress navigation menus — create, read, update, and delete menus, menu items, and menu location assignments. Your AI agent can manage site navigation without touching the WordPress admin.

## Menu Operations

### Listing Menus

```
List all navigation menus on this site.
```

The agent returns all registered menus with their assigned theme locations:

```json
{
  "menus": [
    {
      "id": 3,
      "name": "Main Menu",
      "slug": "main-menu",
      "location": "primary",
      "items_count": 7
    },
    {
      "id": 5,
      "name": "Footer Links",
      "slug": "footer-links",
      "location": "footer",
      "items_count": 4
    }
  ]
}
```

### Creating Menus

```
Create a new menu called "Services Menu".
```

The agent calls `elementeer_create_menu` with the menu name:

```json
{
  "name": "Services Menu",
  "description": "Service pages navigation"
}
```

### Menu Locations

WordPress themes register menu locations (primary, footer, social, mobile). Elementeer reads and assigns them:

```
Assign the "Main Menu" to the primary location and "Footer Links" to the footer location.
```

Available operations:

| Operation | Tool | Description |
|-----------|------|-------------|
| List locations | `elementeer_list_menu_locations` | All registered theme locations |
| Assign location | `elementeer_assign_menu_location` | Map a menu to a theme location |
| Unassign location | `elementeer_assign_menu_location` | Pass `menu_id: 0` to unassign |

## Menu Items

### Listing Items

```
Show me all items in the main menu with their hierarchy.
```

The agent returns the menu tree with parent-child relationships:

```json
{
  "menu_id": 3,
  "items": [
    {
      "id": 12,
      "title": "Home",
      "url": "/",
      "type": "custom",
      "parent": 0,
      "position": 1,
      "children": []
    },
    {
      "id": 13,
      "title": "Services",
      "url": "/services",
      "type": "page",
      "object_id": 42,
      "parent": 0,
      "position": 2,
      "children": [
        {
          "id": 15,
          "title": "Web Design",
          "url": "/services/web-design",
          "type": "page",
          "object_id": 45,
          "parent": 13,
          "position": 1,
          "children": []
        },
        {
          "id": 16,
          "title": "SEO",
          "url": "/services/seo",
          "type": "page",
          "object_id": 46,
          "parent": 13,
          "position": 2,
          "children": []
        }
      ]
    },
    {
      "id": 14,
      "title": "Contact",
      "url": "/contact",
      "type": "page",
      "object_id": 44,
      "parent": 0,
      "position": 3,
      "children": []
    }
  ]
}
```

### Adding Items

Add menu items of any type:

```
Add a "Blog" page to the main menu after the Services item.
```

Item types supported:

| Type | Description |
|------|-------------|
| `custom` | Custom URL with arbitrary title |
| `page` | Link to a WordPress page |
| `post` | Link to a WordPress post |
| `category` | Link to a post category |
| `post_type_archive` | Link to a post type archive |

```
Add a custom link "External Docs" pointing to docs.example.com as a child of the Services item.
```

Specify the parent item ID to create nested structures.

### Updating Items

```
Change the "Services" menu item title to "What We Do" and update its URL to /what-we-do.
```

### Reordering

```
Move the "Contact" item to be first in the main menu.
```

### Deleting Items

```
Remove the "External Docs" item from the Services submenu.
```

!!! warning "Menu item deletion is L2"
    Deleting menu items is governed at L2 — the operation is queued for review
    before execution.

## Menu Item Properties

Each menu item supports these properties:

| Property | Description |
|----------|-------------|
| `title` | Display text |
| `url` | Link destination (for custom links) |
| `object_type` | Linked object type (`page`, `post`, `category`, `custom`) |
| `object_id` | ID of the linked object |
| `parent` | Parent menu item ID for hierarchy |
| `position` | Order within siblings |
| `target` | Link target (`_self` or `_blank`) |
| `classes` | CSS classes (space-separated) |
| `attr_title` | Title attribute (tooltip) |
| `description` | Item description for accessibility |

## Batch Menu Operations

Create a complete menu structure in one session:

```
Create the main navigation:
- Home (page ID 1)
- About (page ID 2)
- Services (page ID 3) with children: Web Design, SEO, Marketing
- Blog (page ID 45)
- Contact (page ID 46)
Assign this menu to the primary location.
```

The agent creates the menu, adds all items with proper hierarchy, and assigns it to the theme location — all in a sequence of tool calls.

# Voxel Marketplace Integration

Elementeer integrates with the **Voxel** marketplace plugin for WordPress, providing AI agent access to listings, orders, memberships, search, and reviews. Voxel is a dynamic post type and listing management system built for directory and marketplace sites.

## Detection and Status

```
Check if Voxel is installed and what version is active.
```

Elementeer auto-detects Voxel and reports:

```json
{
  "voxel": {
    "installed": true,
    "active": true,
    "version": "2.0.0",
    "post_types": 4,
    "listings": 342,
    "template_count": 18
  }
}
```

## Free Tier: Listing CRUD & Product Types

The Free tier of Elementeer includes core Voxel operations:

### Post Types and Fields

Voxel uses dynamic post types with custom fields. Elementeer reads and manages them:

```
List all Voxel post types and their custom fields.
```

```json
{
  "post_types": [
    {
      "key": "business",
      "label": "Businesses",
      "fields": [
        { "key": "business_name", "type": "text", "required": true },
        { "key": "logo", "type": "image" },
        { "key": "category", "type": "taxonomy" },
        { "key": "website", "type": "url" },
        { "key": "phone", "type": "text" },
        { "key": "rating", "type": "number" }
      ]
    },
    {
      "key": "event",
      "label": "Events",
      "fields": [
        { "key": "event_name", "type": "text" },
        { "key": "date", "type": "date" },
        { "key": "location", "type": "location" }
      ]
    }
  ]
}
```

### Listing Operations

```
List the 20 most recent business listings.
```

```
Create a new business listing for "Acme Coffee Roasters" with 
category "Food & Drink", website "acmecoffee.com", and phone "555-0123".
```

```json
{
  "post_type": "business",
  "title": "Acme Coffee Roasters",
  "fields": {
    "business_name": "Acme Coffee Roasters",
    "category": [12],
    "website": "https://acmecoffee.com",
    "phone": "555-0123"
  },
  "status": "publish"
}
```

### Taxonomy Management

Voxel uses custom taxonomies for listing categories, tags, and filters:

```
List all categories in the "Business Type" taxonomy.
```

```
Add a new category "Coffee Shops" to the Business Type taxonomy.
```

## Pro Tier: Full Marketplace Operations

The Advanced tier (`@elementeer/pro`) unlocks:

### Order Management

```
Show all Voxel orders from the last 30 days with status "completed".
```

### Membership Management

```
List active memberships and their expiration dates.
```

```
Extend the membership for user ID 45 by 30 days.
```

### Search Management

Voxel's search system indexes listings for faceted search. Elementeer can:

```
Reindex all business listings in the Voxel search index.
```

### Review Management

```
Show reviews for listing ID 234, sorted by most recent.
```

```
Moderate the review by user 67 on listing 234 — approve it.
```

## Voxel Templates

Voxel uses Elementor templates for listing cards, single listing pages, and archive layouts. Elementeer manages these through the standard template tools:

```
List all Voxel-related templates in the Elementor library.
```

```
Import a new "Business Card" template for the business listing archive.
```

## Data Mapping

Elementeer maps Voxel's dynamic field system to structured, typed access:

| Voxel Field Type | Elementeer Representation |
|-----------------|--------------------------|
| `text` | String |
| `textarea` | String |
| `url` | String (validated URL) |
| `email` | String (validated email) |
| `number` | Number |
| `date` | ISO 8601 date string |
| `image` | Attachment ID + URL |
| `file` | Attachment ID + URL |
| `location` | Lat/Lng + address object |
| `taxonomy` | Array of term IDs |
| `repeater` | Array of field group objects |
| `relation` | Post ID reference |

## Governance Considerations

Voxel marketplace operations follow Elementeer's governance model:

- **L1:** Reading listings, post types, fields, and taxonomies
- **L1:** Creating and updating individual listings
- **L2:** Bulk listing operations, search reindexing
- **L2:** Review moderation
- **L3:** Membership and payment-related changes

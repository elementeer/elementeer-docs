# WooCommerce Integration

The WooCommerce integration (Advanced tier) gives your AI agent full access to store data — products, orders, categories, settings, and reports. The integration uses WooCommerce's native data structures and respects WooCommerce hooks and filters.

!!! info "Advanced Tier Feature"
    The WooCommerce integration requires the `@elementeer/pro` addon plugin on your
    WordPress site. See [Product Tiers](../concepts-tiers.md) for details.

## Detection

Elementeer auto-detects WooCommerce on activation and exposes WooCommerce tools when the plugin is active:

```
Check if WooCommerce is installed and active on this site.
```

```json
{
  "woocommerce": {
    "installed": true,
    "active": true,
    "version": "9.4.0",
    "products": 156,
    "orders": 423,
    "categories": 12
  }
}
```

## Product Management

### Listing Products

```
List the 10 most recent products with their prices and stock status.
```

```json
{
  "products": [
    {
      "id": 204,
      "name": "Premium Widget",
      "sku": "WDG-001",
      "price": "49.99",
      "stock_status": "instock",
      "stock_quantity": 23,
      "categories": ["Widgets", "Premium"]
    }
  ],
  "total": 156
}
```

### Creating Products

```
Create a new simple product: "Ergonomic Keyboard" at $129.99, SKU KB-ERG-002, 
15 in stock, in the Keyboards category.
```

The agent calls `woocommerce_create_product`:

```json
{
  "name": "Ergonomic Keyboard",
  "type": "simple",
  "regular_price": "129.99",
  "sku": "KB-ERG-002",
  "stock_quantity": 15,
  "categories": ["Keyboards"],
  "description": "Premium ergonomic mechanical keyboard with split design."
}
```

Supported product types:

| Type | Description |
|------|-------------|
| `simple` | Standard product with no variations |
| `variable` | Product with variations (size, color, etc.) |
| `grouped` | Group of related products |
| `external` | External/affiliate product |
| `virtual` | Non-physical product (no shipping) |
| `downloadable` | Digital product with file downloads |

### Updating Products

```
Update the price of product ID 204 to $54.99 and increase stock to 50.
```

```
Add a sale price of $39.99 to the Premium Widget, valid through end of month.
```

### Product Images

```
Add product images to the Ergonomic Keyboard from the media library.
```

Elementeer manages product images, gallery images, and image ordering through the media library integration.

## Order Management

### Listing Orders

```
Show me orders from the last 7 days with status "processing".
```

```json
{
  "orders": [
    {
      "id": 1092,
      "status": "processing",
      "total": "149.97",
      "currency": "USD",
      "customer": "jane@example.com",
      "items": 2,
      "date": "2026-07-16T14:22:00Z"
    }
  ],
  "total_orders": 12,
  "period": "2026-07-10 to 2026-07-17"
}
```

### Order Details

```
Show me the full details of order ID 1092.
```

Returns complete order data: line items, shipping address, billing address, payment method, coupons applied, and order notes.

### Order Status Management

```
Mark order 1092 as completed and add a note "Shipped via FedEx #FX-88234".
```

Supported status transitions: `pending` → `processing` → `completed`, and `on-hold`, `cancelled`, `refunded`, `failed`.

## Category Management

```
List all product categories with product counts.
```

```
Create a new category "Accessories" under "Keyboards".
```

## Store Settings

```
What are my current WooCommerce store settings?
```

Elementeer reads and writes WooCommerce settings:

| Setting Group | What It Covers |
|--------------|---------------|
| General | Store address, currency, selling locations |
| Products | Weight/dimension units, review settings, inventory |
| Tax | Tax rates, tax display, tax classes |
| Shipping | Shipping zones, methods, options |
| Payments | Active payment gateways and their settings |
| Accounts | Registration, privacy, account endpoints |
| Emails | Email notifications, sender, templates |

!!! warning "Settings changes are L2/L3"
    Store-level configuration changes are governed at L2 (impactful changes)
    with L3 for payment and tax settings.

## Product Variations

For variable products, manage attribute terms and variations:

```
List all variations of product ID 300 with their prices and stock.
```

```
Add a new variation to the "T-Shirt" product: Large, Blue, $29.99, 25 in stock.
```

## Reports and Analytics

```
What are my top 5 selling products this month?
```

```
Show monthly revenue for the last 6 months.
```

The agent generates summary reports from WooCommerce order data — no separate analytics plugin required.

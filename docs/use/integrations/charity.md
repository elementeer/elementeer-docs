# Charity Plugins Integration

Elementeer integrates with WordPress charity and donation plugins — GiveWP and Charitable. Your AI agent can detect active charity platforms, read donation forms, and analyze fundraising data.

## Supported Plugins

| Plugin | Detection | Capabilities |
|--------|-----------|-------------|
| **GiveWP** | give | Donation forms, donors, donations, stats, goals |
| **Charitable** | charitable | Campaigns, donations, donors |

## GiveWP Integration

GiveWP is the most popular WordPress donation plugin. Elementeer auto-detects it:

```
Check if GiveWP is installed and show fundraising stats.
```

### Detection and Status

```json
{
  "givewp": {
    "active": true,
    "version": "3.16",
    "forms": 4,
    "total_donations": 312,
    "total_revenue": "48,250.00",
    "donors": 187
  }
}
```

### Donation Forms

```
List all active GiveWP donation forms with their goals and progress.
```

```json
{
  "forms": [
    {
      "id": 5,
      "title": "Annual Fundraiser 2026",
      "goal": "25000.00",
      "raised": "18200.00",
      "progress": "72.8%",
      "donations": 134,
      "status": "publish"
    },
    {
      "id": 6,
      "title": "Monthly Giving Program",
      "goal": "5000.00",
      "raised": "3200.00",
      "progress": "64%",
      "donations": 47,
      "status": "publish"
    }
  ]
}
```

### Donation Stats

```
Show donation stats for the current year — total, monthly breakdown, top donors.
```

```json
{
  "year": 2026,
  "total_donations": 187,
  "total_revenue": "28,150.00",
  "average_donation": "150.53",
  "monthly": {
    "January": { "donations": 31, "revenue": "4,650.00" },
    "February": { "donations": 28, "revenue": "4,200.00" }
  },
  "top_donors": [
    { "name": "Alice Johnson", "total": "2,500.00", "donations": 4 },
    { "name": "Bob Williams", "total": "1,800.00", "donations": 1 }
  ]
}
```

### Donor Information

```
Show recent donors and their giving history.
```

### Form Performance

```
Which donation form has the highest conversion rate?
```

The agent analyzes form views vs completions:

```json
{
  "forms": [
    {
      "id": 5,
      "title": "Annual Fundraiser 2026",
      "views": 1240,
      "donations": 134,
      "conversion_rate": "10.8%",
      "average_donation": "135.82"
    }
  ]
}
```

## Charitable Integration

Charitable is a campaign-focused donation plugin:

```
List all active Charitable campaigns with their fundraising progress.
```

```json
{
  "campaigns": [
    {
      "id": 8,
      "title": "Community Garden Project",
      "goal": "15000.00",
      "raised": "11200.00",
      "progress": "74.7%",
      "donors": 89,
      "end_date": "2026-09-30"
    }
  ]
}
```

### Campaign Details

```
Show full details for campaign ID 8 — description, donor list, recent donations.
```

### Donor Management

```
List all donors who gave more than $500 this year.
```

## Elementor Integration

Charity plugins often use Elementor for donation form pages and campaign landing pages. Elementeer bridges the two:

```
List all Elementor templates used on GiveWP donation form pages.
```

```
Update the donation form template to match the new brand colors.
```

## Reporting and Analytics

Generate cross-plugin reports:

```
Summarize all fundraising activity across GiveWP and Charitable for Q2 2026.
```

The agent aggregates data from all active charity plugins into a unified report.

## Governance

Charity plugin operations follow Elementeer's governance:

- **L0:** Reading forms, campaigns, stats, donors
- **L1:** Updating form settings, campaign details
- **L2:** Modifying donation records
- **L3:** Deleting campaigns with donation history

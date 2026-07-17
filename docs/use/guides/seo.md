# SEO Operations

Elementeer provides unified SEO tooling that works across multiple SEO plugins — Yoast, RankMath, SEOPress, and AIOSEO — through a single, consistent interface. Your AI agent reads and writes SEO metadata, analyzes content, and identifies optimization opportunities without worrying about which plugin is active.

## Multi-Plugin Support

Elementeer auto-detects the active SEO plugin and uses the correct API:

| Plugin | Detection | Capabilities |
|--------|-----------|-------------|
| **Yoast SEO** | WordPress SEO by Yoast | Full read/write meta, focus keywords, readability, schema |
| **RankMath** | Rank Math SEO | Full read/write meta, focus keywords, schema, 404 monitor |
| **SEOPress** | SEOPress | Meta read/write, social metadata, XML sitemap |
| **AIOSEO** | All in One SEO | Meta read/write, TruSEO scoring, local SEO |

The agent doesn't need to know which plugin you're using — Elementeer handles the mapping internally.

## SEO Analysis

Run a comprehensive SEO analysis on any page:

```
Analyze the SEO of the homepage.
```

The agent calls `elementeer_analyze_seo` which returns:

```json
{
  "page_id": 7,
  "url": "https://example.com",
  "score": 78,
  "checks": {
    "meta_title": {
      "status": "pass",
      "value": "Acme Corp — Enterprise Software Solutions",
      "length": 47,
      "optimal": true
    },
    "meta_description": {
      "status": "fail",
      "value": "",
      "message": "No meta description set"
    },
    "focus_keyword": {
      "status": "pass",
      "value": "enterprise software",
      "density": 2.3
    },
    "heading_hierarchy": {
      "status": "warning",
      "message": "H1 found but multiple H1 tags detected on page"
    },
    "images": {
      "status": "warning",
      "total": 12,
      "missing_alt": 4
    },
    "internal_links": {
      "status": "pass",
      "count": 7
    },
    "readability": {
      "status": "pass",
      "flesch_score": 65,
      "grade": "8th-9th grade"
    }
  },
  "recommendations": [
    "Add a meta description (recommended length: 120-155 characters)",
    "Ensure only one H1 heading per page",
    "Add alt text to 4 images"
  ]
}
```

## Reading SEO Metadata

```
Show me the SEO title and description for the Services page.
```

The agent reads plugin-specific metadata and normalizes it:

```json
{
  "post_id": 42,
  "seo_title": "Web Design & Development Services — Acme Corp",
  "seo_description": "Professional web design and development services. Custom WordPress sites, Elementor expertise, and ongoing support.",
  "focus_keyword": "web design services",
  "canonical_url": "https://example.com/services",
  "noindex": false,
  "nofollow": false,
  "og_title": "Web Design Services — Acme Corp",
  "og_description": "Custom WordPress designs that convert.",
  "og_image": "https://example.com/wp-content/uploads/services-og.jpg",
  "twitter_card": "summary_large_image"
}
```

## Writing SEO Metadata

```
Set the SEO title for the About page to "About Acme Corp — Our Story & Team" 
and the meta description to "Learn about Acme Corp's mission, team, and 15-year 
history of enterprise software innovation."
```

The agent calls `elementeer_update_page` with SEO fields:

```json
{
  "id": 15,
  "seo_title": "About Acme Corp — Our Story & Team",
  "seo_description": "Learn about Acme Corp's mission, team, and 15-year history of enterprise software innovation.",
  "focus_keyword": "about acme corp"
}
```

!!! tip "Character limits"
    Elementeer validates title (50-60 chars) and description (120-155 chars) lengths
    against SEO best practices. The agent will warn you if your values exceed
    recommended limits.

## Focus Keyword Optimization

```
Check if the focus keyword "enterprise software" appears in the homepage title, 
headings, and first paragraph.
```

The agent analyzes keyword usage and reports:

- Keyword presence in SEO title
- Keyword presence in H1
- Keyword presence in first paragraph
- Keyword density across the page content
- Keyword appearance in image alt text
- Keyword in URL slug

## Readability Analysis

```
Analyze the readability of the About page.
```

The readability report includes:

- **Flesch Reading Ease** score
- **Sentence length** average and maximum
- **Paragraph length** average
- **Passive voice** percentage
- **Transition words** usage
- **Consecutive sentences** starting with the same word

## Bulk SEO Operations

Apply SEO metadata across multiple pages:

```
Set the same focus keyword "acme services" on all service subpages.
```

```
Find all pages with empty meta descriptions and generate appropriate ones.
```

The agent lists affected pages, then updates each with the `elementeer_update_page` tool. For generating descriptions at scale (Advanced tier), the agent uses AI-powered description generation.

## SEO Plugin-Specific Features

Elementeer exposes plugin-specific capabilities through a unified interface:

### Yoast-Specific
- Readability scores (Flesch)
- Cornerstone content flag
- Breadcrumb title

### RankMath-Specific
- SEO score breakdown (100-point scale)
- 404 monitor integration
- Schema type and data

### SEOPress-Specific
- Social network metadata (OG, Twitter cards)
- XML/HTML sitemap status
- Google Analytics integration status

### AIOSEO-Specific
- TruSEO page analysis
- Local SEO data
- Robots.txt editor status

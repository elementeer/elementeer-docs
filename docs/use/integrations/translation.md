# Translation Integration

Elementeer integrates with multilingual WordPress setups — WPML and Polylang — to provide translation coverage analysis and AI-powered batch translation. Your AI agent can audit translation completeness, identify gaps, and (on Advanced tier) translate content across languages.

## Supported Plugins

| Plugin | Detection | Capabilities |
|--------|-----------|-------------|
| **WPML** | sitepress-multilingual-cms | Language detection, coverage analysis, translation status |
| **Polylang** | polylang | Language detection, coverage analysis, content linking |

## WPML Integration

WPML is a comprehensive multilingual plugin. Elementeer detects it and provides translation intelligence:

```
Check if WPML is installed and analyze translation coverage across the site.
```

### Detection and Status

```json
{
  "wpml": {
    "active": true,
    "version": "4.7",
    "languages": ["en", "de", "fr", "es"],
    "default_language": "en",
    "translated_content": {
      "pages": { "total": 24, "fully_translated": 18, "partially": 4, "untranslated": 2 },
      "posts": { "total": 45, "fully_translated": 30, "partially": 10, "untranslated": 5 },
      "templates": { "total": 47, "fully_translated": 12, "partially": 0, "untranslated": 35 }
    }
  }
}
```

### Coverage Analysis

```
Which pages have incomplete German translations?
```

```json
{
  "language": "de",
  "incomplete": [
    {
      "source_id": 45,
      "title": "Services",
      "translated": false,
      "reason": "No translation exists"
    },
    {
      "source_id": 46,
      "title": "Contact",
      "translated": true,
      "elements": {
        "title": "Kontakt",
        "content": "[empty]",
        "status": "needs_translation_content"
      }
    }
  ]
}
```

### Template Translation Status

Elementor templates in WPML require special handling:

```
How many Elementor templates have translations in each language?
```

```json
{
  "template_translations": {
    "en": 47,
    "de": 12,
    "fr": 8,
    "es": 5,
    "coverage": {
      "de": "25.5%",
      "fr": "17.0%",
      "es": "10.6%"
    }
  }
}
```

## AI Batch Translation (Advanced Tier)

The Advanced tier adds AI-powered batch translation. Your agent can translate content across languages while preserving Elementor widget structure:

```
Translate the homepage and all service pages into German and French.
```

The agent:

1. Identifies source content for each page
2. Calls the AI translation service for each language pair
3. Creates translated pages/posts in WPML/Polylang
4. Preserves Elementor widget settings, links, and media references
5. Sets translation status in the multilingual plugin

```json
{
  "source_language": "en",
  "target_languages": ["de", "fr"],
  "pages": [7, 42, 43, 44, 45],
  "options": {
    "preserve_links": true,
    "translate_media_alt": true,
    "translate_meta": true
  }
}
```

!!! warning "AI Translation Validation"
    AI translations should be reviewed by a human before publishing. Elementeer
    creates translations in draft status by default. The Governance model queues
    batch translations at L2 for approval.

## Polylang Integration

Polylang provides lightweight multilingual support. Elementeer detects it:

```
Check Polylang language configuration and content coverage.
```

```json
{
  "polylang": {
    "active": true,
    "version": "3.6",
    "languages": ["en", "nl", "fr"],
    "default_language": "en",
    "content": {
      "pages": 18,
      "posts": 32,
      "translation_coverage": "72%"
    }
  }
}
```

### Language Link Management

```
Show which pages have translations linked in Polylang for the Dutch language.
```

### Content Sync

```
Find English pages that don't have any translation linked in Polylang.
```

## Elementor-Specific Translation Intelligence

Elementeer has deep knowledge of how Elementor stores translatable content:

- **Widget text content** — headings, text editors, buttons
- **Media references** — image URLs are typically shared across translations
- **Global styles** — colors and typography are site-wide; translation only affects content
- **Template references** — templates can be translated independently of pages

This intelligence ensures AI translations preserve the design while only translating the content.

## SEO for Multilingual Sites

```
Check SEO metadata across all language versions of the homepage.
```

The agent reads SEO titles and descriptions for each language version and reports inconsistencies or missing data.

## Governance

Translation operations follow Elementeer's governance:

- **L0:** Reading translation status and coverage
- **L1:** Individual page translations
- **L2:** Batch translations (queued for review)
- **L2:** AI translation operations (require approval before publishing)

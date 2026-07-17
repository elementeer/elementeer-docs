# Accessibility Integration

Elementeer provides automated WCAG accessibility scanning and remediation for Elementor-powered sites. Your AI agent can scan pages for accessibility violations, auto-fix common issues, and integrate with dedicated accessibility plugins.

## WCAG Scanning

Run a comprehensive accessibility scan against any page:

```
Run a WCAG 2.1 AA accessibility scan on the homepage.
```

The agent calls `elementeer_scan_page_accessibility` which returns:

```json
{
  "page_id": 7,
  "standard": "wcag21aa",
  "score": 84,
  "violations": {
    "critical": [
      {
        "rule": "color-contrast",
        "description": "Text contrast ratio of 3.2:1 is below the minimum 4.5:1 required",
        "elements": [
          {
            "selector": ".hero-section .hero-subtitle",
            "current_ratio": "3.2:1",
            "required_ratio": "4.5:1",
            "suggested_fix": "Change text color from #A8B0C4 to #7F87A0"
          }
        ]
      }
    ],
    "serious": [
      {
        "rule": "image-alt",
        "description": "Image missing alternative text",
        "elements": [
          {
            "selector": ".team-section img:first-child",
            "suggested_fix": "Add descriptive alt text to this team photo"
          }
        ]
      },
      {
        "rule": "label",
        "description": "Form input missing associated label",
        "elements": [
          {
            "selector": ".newsletter-form input[type='email']",
            "suggested_fix": "Add a <label> or aria-label to this email input"
          }
        ]
      }
    ],
    "moderate": [],
    "minor": []
  },
  "auto_fixable": ["image-alt", "label"],
  "needs_review": ["color-contrast"]
}
```

## Accessibility Standards

Elementeer supports multiple WCAG levels:

| Standard | Description |
|----------|-------------|
| `wcag2a` | WCAG 2.0 Level A |
| `wcag2aa` | WCAG 2.0 Level AA (most common legal standard) |
| `wcag21a` | WCAG 2.1 Level A |
| `wcag21aa` | WCAG 2.1 Level AA |
| `wcag22aa` | WCAG 2.2 Level AA |
| `section508` | US Section 508 compliance |

## Auto-Fix

For common violations, Elementeer can apply fixes automatically:

```
Fix all auto-fixable accessibility issues on the homepage.
```

The agent calls `elementeer_apply_accessibility_fixes` which handles:

| Rule | Auto-Fix Action |
|------|----------------|
| `image-alt` | Adds descriptive alt text based on image context and filename |
| `color-contrast` | Adjusts text colors to meet minimum contrast ratios |
| `label` | Adds aria-label attributes to unlabeled form inputs |
| `heading-order` | Corrects heading hierarchy (H1 → H2 → H3) |
| `document-title` | Ensures page has a title element |
| `html-lang-valid` | Adds or corrects lang attribute on HTML element |

!!! tip "Review before applying"
    Auto-fixes are safe but not perfect. Review color contrast changes and alt text
    suggestions before applying them to production pages. The Governance model queues
    auto-fix operations at L2 for approval.

## Batch Scanning

Scan multiple pages at once:

```
Run accessibility scans on all top-level pages and give me a summary.
```

The agent scans each page and produces a summary:

```json
{
  "pages_scanned": 12,
  "average_score": 79,
  "critical_issues": 3,
  "serious_issues": 18,
  "worst_page": {
    "id": 15,
    "title": "About Us",
    "score": 62,
    "critical": 2,
    "serious": 5
  }
}
```

## Ally Integration

Elementeer detects and integrates with the **Ally** accessibility plugin when active:

```
Check if Ally is active and show its accessibility configuration.
```

Ally provides additional accessibility features that Elementeer reads and reports on:

- Focus outline styles
- Skip navigation links
- Keyboard navigation enhancements
- Screen reader text

## Pre-Launch Checklist

Use accessibility scanning as part of your site launch process:

```
Run a pre-launch accessibility checklist: scan all published pages, 
ensure no critical violations, and auto-fix any remaining image-alt issues.
```

The checklist ensures you meet accessibility standards before going live.

## Continuous Accessibility Monitoring

Integrate accessibility scanning into CI/CD:

```bash
# Pre-deploy accessibility gate
elementeer-mcp scan-accessibility --page-id 7 --json > a11y.json
VIOLATIONS=$(jq '.violations.critical | length' a11y.json)
if [ "$VIOLATIONS" -gt 0 ]; then
  echo "$VIOLATIONS critical accessibility violations detected"
  exit 1
fi
```

## Governance

Accessibility operations follow Elementeer's governance:

- **L0:** Scanning and reporting (no changes)
- **L1:** Individual element fixes
- **L2:** Batch auto-fixes across multiple pages

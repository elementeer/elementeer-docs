# Site Assessment

Elementeer's site assessment tool analyzes your Elementor-powered WordPress site across 10 data categories and produces a prioritized report with actionable recommendations. It's the fastest way to understand the health, structure, and opportunities of any Elementor installation.

## What It Analyzes

The assessment engine collects data across these categories:

| # | Category | What It Checks |
|---|----------|---------------|
| 1 | **WordPress Core** | Version, debug mode, permalink structure, REST API status, cron health |
| 2 | **Elementor** | Version (Free/Pro), experiment status, CSS print method, editor loader |
| 3 | **Plugins** | Active plugin inventory, known conflicts with Elementor, update status |
| 4 | **Templates** | Count by type, unused templates, Elementor library sync status |
| 5 | **Pages & Content** | Pages using Elementor vs other editors, Elementor canvas usage |
| 6 | **Global Styles** | Kit configuration, color palette completeness, typography system |
| 7 | **SEO** | Active SEO plugin detection, meta coverage, heading hierarchy analysis |
| 8 | **Performance** | CSS cache status, render-blocking resources, image optimization gaps |
| 9 | **Accessibility** | WCAG baseline checks, ARIA attribute presence, contrast issues |
| 10 | **Addons** | Elementor addon detection, compatibility with Elementeer integrations |

## Running an Assessment

From your AI agent:

```
Run a full site assessment and give me the top issues.
```

The agent calls `elementeer_run_assessment` which returns a structured report:

```json
{
  "site": {
    "url": "https://example.com",
    "wordpress": "6.7",
    "elementor": "3.28.0",
    "elementor_pro": true
  },
  "score": 72,
  "categories": {
    "performance": {
      "score": 45,
      "issues": [
        {
          "severity": "high",
          "title": "Elementor CSS cache never flushed",
          "description": "CSS cache hasn't been regenerated in 30+ days.",
          "fix": "Run elementeer_flush_elementor_cache"
        }
      ]
    },
    "seo": {
      "score": 65,
      "issues": [
        {
          "severity": "medium",
          "title": "8 pages missing meta descriptions",
          "description": "Pages without meta descriptions appear less effectively in search results.",
          "fix": "Use elementeer_seo_analyze and elementeer_update_page for each affected page"
        }
      ]
    }
  },
  "recommendations": [
    {
      "priority": 1,
      "category": "performance",
      "action": "Flush Elementor CSS cache",
      "tool": "elementeer_flush_elementor_cache",
      "effort": "instant"
    },
    {
      "priority": 2,
      "category": "seo",
      "action": "Add meta descriptions to 8 untitled pages",
      "tool": "elementeer_update_page",
      "effort": "5 minutes"
    }
  ]
}
```

## Recommendation Engine

Recommendations are prioritized by a rule engine that weighs severity, impact, and effort:

- **Critical:** Site functionality issues (Elementor not loading, REST API broken)
- **High:** Performance problems affecting user experience (cached CSS stale, unoptimized images)
- **Medium:** Content quality gaps (missing meta, missing alt text, unused templates)
- **Low:** Optimization opportunities (plugin updates available, minor style inconsistencies)

Each recommendation includes the specific Elementeer tool to fix it, making the assessment both diagnostic and prescriptive.

## Automated Fixes

The agent can apply recommended fixes directly:

```
Fix all the high-severity issues from the assessment report.
```

The agent works through the recommendation list, calling the appropriate tools for each fix. Governance rules apply — L1 fixes execute immediately, L2 fixes are queued for review.

## Scheduled Assessments

Use CLI or cron to run assessments on a schedule:

```bash
# Daily assessment, output to JSON
elementeer-mcp assess --json > "assessment-$(date +%Y%m%d).json"

# Weekly comparison
elementeer-mcp assess --json --compare last-week.json
```

## Assessment in CI/CD

Integrate assessment into your deployment pipeline to catch regressions:

```yaml
- name: Site Assessment
  run: |
    npx @elementeer/mcp assess --json > assessment.json
    # Fail pipeline if score drops below threshold
    SCORE=$(jq '.score' assessment.json)
    if [ "$SCORE" -lt 70 ]; then
      echo "Assessment score $SCORE is below threshold"
      exit 1
    fi
```

## Elementor-Specific Intelligence

The assessment engine has deep knowledge of Elementor internals:

- Detects **CSS print method** (internal vs external file) and recommends the optimal setting
- Identifies **unused Elementor experiments** that may affect rendering
- Reports **widget usage patterns** across templates and pages
- Checks **Elementor Kit** for missing or inconsistent design tokens
- Validates **display conditions** on Theme Builder templates

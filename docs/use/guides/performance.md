# Performance

Elementeer provides tools to keep Elementor-powered WordPress sites running fast — CSS cache management, database cleanup, performance reporting, and (on Advanced tier) Critical CSS generation.

## Elementor CSS Cache

Elementor generates CSS files for each page and template. Over time, this cache can accumulate stale files. Elementeer provides cache management:

### Flush Cache

```
Flush the Elementor CSS cache and regenerate it.
```

The agent calls `elementeer_flush_elementor_cache`. This:

1. Clears all Elementor-generated CSS files from `wp-content/uploads/elementor/css/`
2. Triggers CSS regeneration for all pages and templates
3. Clears the Elementor cache in the WordPress database

```json
{
  "action": "flush",
  "files_removed": 47,
  "files_regenerated": 47,
  "duration_ms": 3200
}
```

!!! info "When to flush"
    Flush the cache after significant template changes, global style updates,
    or when pages display with broken styling after an Elementor update.

### Cache Status

```
Check the Elementor CSS cache status.
```

Reports cache file count, total size, oldest file date, and any known issues:

```json
{
  "status": "healthy",
  "files": 47,
  "total_size": "1.2 MB",
  "oldest_file": "2026-06-15",
  "css_print_method": "external_file"
}
```

## Database Cleanup

Elementor stores revision data, transient data, and optimization metadata in the WordPress database. Elementeer can clean these:

```
Clean up Elementor's database entries — revisions, transients, and orphaned data.
```

| Cleanup Target | Description |
|---------------|-------------|
| Elementor revisions | Redundant post revisions stored by Elementor |
| Transient data | Expired Elementor transients in wp_options |
| Orphaned metadata | Elementor meta for deleted posts |
| CSS cache records | Database entries pointing to removed CSS files |

!!! warning "Database cleanup is L2"
    Database cleanup operations are governed at L2 and require approval before execution.

## Performance Report

```
Generate a performance report for the homepage.
```

The agent calls `elementeer_analyze_performance` which checks:

| Check | What It Measures |
|-------|-----------------|
| Page weight | Total page size including assets |
| Image optimization | Unoptimized images, missing dimensions, format suggestions |
| CSS delivery | Render-blocking CSS, unused CSS detection |
| JS delivery | Render-blocking JavaScript, deferred loading |
| Caching status | Browser caching headers, page caching status |
| Elementor specifics | CSS print method, experiment status, widget count |

```json
{
  "page_id": 7,
  "score": 82,
  "metrics": {
    "page_weight": "1.8 MB",
    "requests": 34,
    "images_unoptimized": 3,
    "render_blocking_css": true,
    "caching_enabled": true
  },
  "recommendations": [
    {
      "priority": "high",
      "action": "Optimize 3 large images (saves ~400KB)",
      "tool": "elementeer_analyze_images"
    },
    {
      "priority": "medium",
      "action": "Enable Elementor's 'Improved CSS Loading' experiment",
      "tool": "elementeer_update_elementor_settings"
    }
  ]
}
```

## Image Optimization

```
Analyze images across the site and identify optimization opportunities.
```

The agent calls `elementeer_analyze_images` which scans the media library for:

- Uncompressed images (>500KB)
- PNG files that should be WebP
- Missing width/height attributes (affecting CLS)
- Images larger than their display dimensions

## Elementor Performance Experiments

Elementor includes experimental performance features. Elementeer reads and manages them:

```
Check which Elementor performance experiments are active.
```

Key experiments:

| Experiment | Benefit | Recommended |
|-----------|---------|-------------|
| Improved CSS Loading | Reduces render-blocking CSS | Yes |
| Optimized DOM Output | Reduces HTML bloat | Yes |
| Inline Font Icons | Eliminates Font Awesome CSS file | Yes |
| Improved Asset Loading | Deferred JS loading | Yes |
| Flexbox Container | Modern layout engine | Yes |

```
Enable the improved CSS loading and optimized DOM output experiments.
```

## Critical CSS (Advanced Tier)

Critical CSS extracts the CSS needed for above-the-fold content and inlines it in the `<head>`, while loading the full stylesheet asynchronously. This improves First Contentful Paint (FCP) and Largest Contentful Paint (LCP).

```
Generate and inject Critical CSS for the homepage.
```

The Critical CSS tool:

1. Analyzes the page's above-the-fold content
2. Extracts only the CSS rules needed to render it
3. Inlines those rules in the document head
4. Defers the full stylesheet loading

## Performance in CI/CD

Integrate performance checks into your deployment pipeline:

```bash
# Check performance score before deploy
elementeer-mcp analyze-performance --page-id 7 --json | jq '.score'

# Fail if score drops
SCORE=$(elementeer-mcp analyze-performance --page-id 7 --json | jq '.score')
if [ "$SCORE" -lt 70 ]; then
  echo "Performance score too low"
  exit 1
fi
```

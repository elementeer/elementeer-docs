# CI/CD Integration

Elementeer's CLI and MCP server are designed for pipeline use. Run site assessments, flush caches, verify health, and manage templates as part of your deployment workflow.

## GitHub Actions

### Basic Health Check

```yaml
name: Site Health Check
on:
  deployment_status:
    types: [success]

jobs:
  health-check:
    runs-on: ubuntu-latest
    steps:
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Health Check
        run: |
          npx @elementeer/mcp@latest health --json
        env:
          ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
          ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

### Post-Deploy Cache Flush

```yaml
name: Post-Deploy Cache Flush
on:
  push:
    branches: [main]

jobs:
  flush-cache:
    runs-on: ubuntu-latest
    steps:
      - name: Flush Elementor CSS Cache
        run: |
          npx @elementeer/mcp@latest flush-cache
        env:
          ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
          ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

### Pre-Release Assessment Gate

```yaml
name: Pre-Release Site Audit
on:
  release:
    types: [published]

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - name: Run Site Assessment
        run: |
          npx @elementeer/mcp@latest assess --json > assessment.json
          SCORE=$(jq '.score' assessment.json)
          echo "Site assessment score: $SCORE"
          if [ "$SCORE" -lt 70 ]; then
            echo "::error::Assessment score $SCORE is below threshold of 70"
            exit 1
          fi
        env:
          ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
          ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

### Accessibility Gate

```yaml
name: Accessibility Check
on:
  pull_request:
    branches: [main]

jobs:
  a11y:
    runs-on: ubuntu-latest
    steps:
      - name: Scan Accessibility
        run: |
          npx @elementeer/mcp@latest scan-accessibility --page-id ${{ vars.HOMEPAGE_ID }} --json > a11y.json
          CRITICAL=$(jq '.violations.critical | length' a11y.json)
          if [ "$CRITICAL" -gt 0 ]; then
            echo "::error::$CRITICAL critical accessibility issues found"
            exit 1
          fi
        env:
          ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
          ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
```

## GitLab CI

```yaml
stages:
  - deploy
  - verify
  - optimize

deploy:
  stage: deploy
  script:
    - ./deploy.sh

health_check:
  stage: verify
  image: node:20
  script:
    - npx @elementeer/mcp@latest health --json
  variables:
    ELEMENTEER_SITE_URL: $ELEMENTEER_SITE_URL
    ELEMENTEER_API_KEY: $ELEMENTEER_API_KEY

cache_flush:
  stage: optimize
  image: node:20
  script:
    - npx @elementeer/mcp@latest flush-cache
  variables:
    ELEMENTEER_SITE_URL: $ELEMENTEER_SITE_URL
    ELEMENTEER_API_KEY: $ELEMENTEER_API_KEY
```

## Bitbucket Pipelines

```yaml
pipelines:
  branches:
    main:
      - step:
          name: Deploy and Verify
          image: node:20
          script:
            - ./deploy.sh
            - npx @elementeer/mcp@latest health --json
            - npx @elementeer/mcp@latest flush-cache
```

## Scheduled Maintenance

Run periodic maintenance operations:

```yaml
name: Weekly Site Maintenance
on:
  schedule:
    - cron: '0 3 * * 0'  # Every Sunday at 3 AM

jobs:
  maintenance:
    runs-on: ubuntu-latest
    steps:
      - name: Run Assessment
        run: npx @elementeer/mcp@latest assess --json > weekly-assessment.json
        env:
          ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
          ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}

      - name: Flush Cache
        run: npx @elementeer/mcp@latest flush-cache
        env:
          ELEMENTEER_SITE_URL: ${{ secrets.WP_URL }}
          ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}

      - name: Store Report
        uses: actions/upload-artifact@v4
        with:
          name: weekly-assessment
          path: weekly-assessment.json
```

## Secrets Management

Always store API keys as secrets:

=== "GitHub Actions"
    ```yaml
    env:
      ELEMENTEER_API_KEY: ${{ secrets.ELEMENTEER_KEY }}
    ```

=== "GitLab CI"
    ```yaml
    variables:
      ELEMENTEER_API_KEY: $ELEMENTEER_API_KEY
    ```

=== "Bitbucket"
    Configure repository variables in **Repository Settings → Pipelines → Repository Variables**

## Multi-Site Pipelines

Run operations across multiple sites:

```yaml
jobs:
  multi-site-check:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        site: [production, staging, client-acme]
    steps:
      - name: Health Check ${{ matrix.site }}
        run: |
          npx @elementeer/mcp@latest --site ${{ matrix.site }} health --json
        env:
          ELEMENTEER_SITE_URL: ${{ secrets[format('{0}_URL', matrix.site)] }}
          ELEMENTEER_API_KEY: ${{ secrets[format('{0}_KEY', matrix.site)] }}
```

## CI/CD Best Practices

- **Use separate API keys** for CI/CD pipelines — scope them to only the capabilities needed
- **Set pipeline keys to Read-Only** when only running assessments and health checks
- **Store keys in secrets** — never hardcode API keys in workflow files
- **Fail fast** — use health checks early in the pipeline to catch connectivity issues
- **Version pin** — use `@elementeer/mcp@latest` or pin to a specific version for reproducibility

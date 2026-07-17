# Elementeer Documentation

Public, user-facing documentation for the Elementeer agent-native Elementor
extension — built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

**Site:** [docs.elementeer.xyz](https://docs.elementeer.xyz)

## Local development

```bash
pip install mkdocs mkdocs-material
mkdocs serve
```

## Build

```bash
mkdocs build --clean --strict
# Output in site/
```

## Deploy

Push to `main` triggers the GitHub Actions deploy workflow, which builds and
publishes to GitHub Pages behind Cloudflare.

## Structure

- `mkdocs.yml` — Site configuration and navigation
- `docs/` — All Markdown content
- `docs/assets/` — Brand CSS, logos, favicon

## Contributing

Internal contributions happen on the canonical Forgejo repo (`git.langevc.com/elementeer/elementeer-docs`).
GitHub is a read-only mirror. See the [Elementeer Internal Docs](https://internal.elementeer.xyz)
for maintainer guidelines.

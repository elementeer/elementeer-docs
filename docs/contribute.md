# Contribute

Elementeer is open-core — the MCP server (Apache-2.0) and WordPress plugin (GPL-2.0) welcome contributions. Development happens on our self-hosted Forgejo instance; the GitHub repositories are public read-only mirrors.

> [!NOTE]
> **Bug reports are welcome via GitHub Issues.** Pull requests are applied upstream on the canonical Forgejo instance and synced back to the GitHub mirrors.

## Ways to Contribute

### Report Bugs

Found an issue? Open a GitHub Issue with:

- Elementeer plugin version
- WordPress version
- Elementor version
- Steps to reproduce
- Expected vs actual behavior

Issues are tracked across the monorepo:

| Component | Repository |
|---|---|
| WordPress Plugin | [github.com/elementeer/elementeer](https://github.com/elementeer/elementeer) |
| MCP Server | [github.com/elementeer/elementeer-mcp](https://github.com/elementeer/elementeer-mcp) |
| Documentation | [github.com/elementeer/elementeer-docs](https://github.com/elementeer/elementeer-docs) |

### Documentation

Improvements to clarity, accuracy, and completeness are always welcome. Open an issue or discussion on the [elementeer-docs repository](https://github.com/elementeer/elementeer-docs).

### Addon Development

Build and publish your own Elementeer addons. The addon system is fully documented — see [Addon Development](publish/addon-development.md). Submit your addon for catalog inclusion by opening an issue.

## Development Setup

The canonical repositories are hosted at `git.langevc.com/elementeer/`. The following clone commands work against the public GitHub mirrors:

### MCP Server (Node.js)

```bash
git clone https://github.com/elementeer/elementeer-mcp.git
cd elementeer-mcp
npm install
npm run dev
```

### WordPress Plugin (PHP)

```bash
git clone https://github.com/elementeer/elementeer.git
cd elementeer
composer install
```

## License

By contributing, you agree that your contributions will be licensed under the same terms as the repository:

- **MCP Server:** Apache-2.0
- **WordPress Plugin:** GPL-2.0
- **Documentation:** CC BY 4.0

See [License](legal/license.md) for full license texts.

## Community

- **GitHub Issues:** [github.com/elementeer/elementeer/issues](https://github.com/elementeer/elementeer/issues)
- **Email:** [hello@elementeer.xyz](mailto:hello@elementeer.xyz)
- **Docs:** [docs.elementeer.xyz](https://docs.elementeer.xyz)

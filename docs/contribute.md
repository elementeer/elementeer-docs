# Contribute

Elementeer is open-core — the MCP server (Apache-2.0) and WordPress plugin (GPL-2.0) welcome contributions. This guide covers how to contribute code, documentation, and integrations.

## Ways to Contribute

### Code Contributions

The [Elementeer MCP server](https://github.com/elementeer/elementeer-mcp) and [WordPress plugin](https://github.com/elementeer/elementeer) are open to contributions:

- **Bug fixes** — found an issue? PRs are welcome
- **New integrations** — add detection and tooling for Elementor-compatible plugins
- **Performance improvements** — optimize the MCP server or REST API
- **Tool additions** — extend the Free tier with new MCP tools

### Documentation

This documentation site lives in the [elementeer-docs repository](https://github.com/elementeer/elementeer-docs). Improvements to clarity, accuracy, and completeness are always welcome:

- Fix typos and unclear language
- Add examples and use cases
- Improve code samples
- Translate documentation

### Addon Development

Build and publish your own Elementeer addons. The addon system is fully documented — see [Addon Development](publish/addon-development.md) for the API. Submit your addon for catalog inclusion by opening an issue.

### Testing & Feedback

Test Elementeer with different WordPress configurations, Elementor versions, and AI agents. Report bugs through GitHub Issues with:

- Elementeer plugin version
- WordPress version
- Elementor version
- Steps to reproduce
- Expected vs actual behavior

## Development Setup

### MCP Server (Node.js)

```bash
git clone https://github.com/elementeer/elementeer-mcp.git
cd elementeer-mcp
npm install
npm run dev
```

The server runs in development mode with hot reload.

### WordPress Plugin (PHP)

```bash
git clone https://github.com/elementeer/elementeer.git
cd elementeer-plugin
composer install
```

Run tests:

```bash
composer test
composer lint
```

### Documentation (MkDocs)

```bash
git clone https://github.com/elementeer/elementeer-docs.git
cd elementeer-docs
pip install -r requirements.txt
mkdocs serve
```

Documentation runs at `http://localhost:8000`.

## Pull Request Process

1. Fork the repository
2. Create a feature branch (`feat/new-tool` or `fix/bug-description`)
3. Write tests for your changes
4. Ensure all existing tests pass
5. Update documentation if your change adds or modifies tools
6. Submit a PR with a clear description

### Commit Style

```
feat: add Voxel membership management tools
fix: resolve 403 on template deletion for admin keys
docs: update Claude Desktop setup instructions for v2.2
test: add integration tests for SEO meta operations
```

### Code Standards

- **PHP:** WordPress coding standards (`phpcs` with WordPress-Extra ruleset)
- **TypeScript:** Prettier + ESLint with strict TypeScript config
- **Documentation:** Markdown, valid MkDocs Material syntax

## License

By contributing, you agree that your contributions will be licensed under the same terms as the repository:

- **MCP Server:** Apache-2.0
- **WordPress Plugin:** GPL-2.0
- **Documentation:** CC BY 4.0

See [License](legal/license.md) for full license texts.

## Community

- **GitHub Issues:** [github.com/elementeer/elementeer-mcp/issues](https://github.com/elementeer/elementeer-mcp/issues)
- **Discussions:** [github.com/elementeer/elementeer-mcp/discussions](https://github.com/elementeer/elementeer-mcp/discussions)
- **Email:** [hello@elementeer.xyz](mailto:hello@elementeer.xyz)

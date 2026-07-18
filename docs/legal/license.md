# License

Elementeer's components are licensed under different terms, reflecting their roles in the open-core architecture.

## Elementeer WordPress Plugin (Core)

**GNU General Public License v2.0 (GPL-2.0)**

The core WordPress plugin is licensed under GPL-2.0, consistent with WordPress's own license. This applies to all code in the elementeer repository at [github.com/elementeer/elementeer](https://github.com/elementeer/elementeer).

GPL-2.0 grants you the right to:

- Use the plugin for any purpose
- Study and modify the source code
- Distribute copies of the original or modified plugin
- Distribute modified versions

All under the condition that any distributed modifications are also licensed under GPL-2.0 and include the source code.

### Why GPL-2.0?

WordPress plugins that interact with WordPress core APIs are generally considered derivative works under the GPL. Using GPL-2.0 ensures full compatibility with the WordPress ecosystem and respects the license of the platform Elementeer extends.

## Elementeer MCP Server

**Apache License 2.0**

The `@elementeer/mcp` npm package is licensed under Apache-2.0. This applies to all code in the [github.com/elementeer/elementeer-mcp](https://github.com/elementeer/elementeer-mcp) repository.

Apache-2.0 grants you the right to:

- Use the server for any purpose, commercial or personal
- Modify and create derivative works
- Distribute the original or modified server
- Sublicense your modifications
- Use any patents held by the contributors

With the requirements to:
- Include a copy of the license in distributions
- State significant changes made to the code
- Preserve copyright, patent, trademark, and attribution notices

### Why Apache-2.0?

The MCP server is a standalone Node.js application that communicates with WordPress via HTTP. It is not a derivative work of WordPress and can be licensed independently. Apache-2.0 provides strong patent protection and is widely adopted in the Node.js ecosystem.

## Elementeer Pro Addon

**Proprietary License**

The `@elementeer/pro` WordPress addon is proprietary. Terms are provided at purchase and included with the addon distribution.

The Pro addon:
- May not be redistributed
- May not be modified or reverse-engineered
- Requires a valid license key per WordPress site

## Elementeer Documentation

**Creative Commons Attribution 4.0 International (CC BY 4.0)**

This documentation is licensed under CC BY 4.0. You may:

- Share — copy and redistribute the material
- Adapt — remix, transform, and build upon the material

Under the condition that you provide attribution to Elementeer.

## Contribution Licensing

By contributing to Elementeer's open-source repositories, you agree that your contributions will be licensed under the same terms as the repository:

- Plugin contributions: GPL-2.0
- MCP Server contributions: Apache-2.0
- Documentation contributions: CC BY 4.0

## Third-Party Components

Elementeer includes third-party open-source components, each under its own license:

| Component | License | Usage |
|-----------|---------|-------|
| Zod | MIT | MCP server input validation |
| WordPress | GPL-2.0 | Plugin runtime environment |
| Elementor | GPL-3.0 | Page builder integration |

Component licenses are included in their respective distribution files and repositories.

## Summary

| Component | License | Source Available |
|-----------|---------|-----------------|
| MCP Server (`@elementeer/mcp`) | Apache-2.0 | Yes — [GitHub](https://github.com/elementeer/elementeer-mcp) |
| WordPress Plugin (core) | GPL-2.0 | Yes — [GitHub](https://github.com/elementeer/elementeer) |
| @elementeer/pro | Proprietary | No |
| Documentation | CC BY 4.0 | Yes — This site |

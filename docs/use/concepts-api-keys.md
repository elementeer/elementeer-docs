# API Keys & Capabilities

API keys are the primary authentication mechanism between the Elementeer MCP server and your WordPress site. Every key is scoped to a set of capabilities that define exactly what operations it can perform.

## Key Structure

An Elementeer API key has the format:

```
elem_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

Keys are generated in WordPress admin under **Settings → Elementeer → API Keys** and displayed only once. Store them securely — they provide authenticated access to your site's Elementeer operations.

## Capability System

Elementeer defines **65 capabilities** organized into **26 groups**. Each capability gates a specific operation or class of operations.

### Capability Groups

| Group | Scope | Example Capabilities |
|-------|-------|---------------------|
| `site` | Site-level operations | `site:read`, `site:assess` |
| `templates` | Elementor templates | `templates:read`, `templates:write`, `templates:delete`, `templates:import` |
| `pages` | WordPress pages | `pages:read`, `pages:write`, `pages:delete` |
| `global_styles` | Elementor kit styles | `global_styles:read`, `global_styles:write` |
| `media` | Media library | `media:read`, `media:upload`, `media:delete` |
| `navigation` | Menus | `navigation:read`, `navigation:write` |
| `seo` | SEO tooling | `seo:read`, `seo:write` |
| `performance` | Cache & optimization | `performance:flush`, `performance:report` |
| `plugins` | Plugin management | `plugins:read`, `plugins:activate` |
| `users` | User operations | `users:read`, `users:write` |
| `settings` | WordPress settings | `settings:read`, `settings:write` |
| `woocommerce` | WooCommerce data | `woocommerce:read`, `woocommerce:write` |
| `voxel` | Voxel marketplace | `voxel:read`, `voxel:write` |
| `booking` | Booking systems | `booking:read`, `booking:write` |
| `lms` | Learning management | `lms:read`, `lms:write` |
| `translation` | AI translation | `translation:read`, `translation:write` |
| `accessibility` | Accessibility tools | `accessibility:scan`, `accessibility:fix` |

Each group typically contains `read`, `write`, and sometimes `delete` sub-capabilities. Additional specialized capabilities exist for operations like bulk imports, snapshots, and design token management.

## Scoping Keys Minimally

Best practice is to create multiple keys, each with the minimum capabilities needed for its use case:

```json
// Read-only key for monitoring dashboards
{
  "name": "Monitoring",
  "capabilities": ["site:read", "templates:read", "pages:read", "media:read"]
}

// CI/CD key for deployment pipelines
{
  "name": "Deploy Pipeline",
  "capabilities": ["templates:write", "performance:flush", "global_styles:write"]
}

// Agent key for day-to-day site management
{
  "name": "Claude Desktop",
  "capabilities": [
    "site:read", "site:assess",
    "templates:read", "templates:write", "templates:import",
    "pages:read", "pages:write",
    "media:read", "media:upload",
    "navigation:read", "navigation:write",
    "seo:read", "seo:write",
    "global_styles:read", "global_styles:write",
    "performance:flush", "performance:report"
  ]
}
```

!!! tip "One key per agent"
    Create a separate API key for each AI agent or pipeline. If one key is compromised,
    you can revoke it without disrupting other workflows.

## Wildcard Keys

For development and testing, you can create a wildcard key with access to all capabilities:

```
capabilities: ["*"]
```

!!! warning "Never use wildcard keys in production"
    A wildcard key bypasses all capability checks. Use it only in local development
    environments. Production keys should always be scoped to specific capability sets.

## Key Management

### Generation

1. Go to **Settings → Elementeer → API Keys**
2. Click **Add New Key**
3. Enter a descriptive name and select capabilities
4. Click **Generate Key**
5. Copy the key — it won't be displayed again

### Revocation

Revoke a compromised or unused key from the API Keys screen. Revocation is immediate — all MCP servers using that key will receive 401 responses on their next request.

### Key Rotation

Rotate keys regularly as part of your security practice:

1. Generate a new key with the same capabilities
2. Update your MCP server configuration with the new key
3. Verify the new key works (`elementeer-mcp health`)
4. Revoke the old key

### Expiration

API keys can be set to expire after a configurable period (30, 90, 180, or 365 days). Expired keys are automatically rejected. Set expiration policies based on your security requirements.

## Security Best Practices

- **Never commit API keys** to version control. Use environment variables or secret management.
- **Use environment variables** for MCP server configuration: `ELEMENTEER_API_KEY` keeps keys out of config files.
- **Rotate keys** quarterly or after team member departures.
- **Audit key usage** from the Elementeer admin dashboard — see which keys are active and when they were last used.
- **Set appropriate expiration** — 90 days is a good default for production keys.

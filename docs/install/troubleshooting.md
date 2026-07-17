# Installation Troubleshooting

Common issues during installation and first connection, with diagnostic steps and solutions.

## REST API 401 — Invalid API Key

**Symptom:** `elementeer-mcp health` returns HTTP 401, or your agent reports authentication errors.

**Diagnosis:**

```bash
# Check if the key is being sent correctly
elementeer-mcp health --verbose
```

**Common causes:**

- API key was copied incorrectly (missing characters, extra whitespace)
- The key was revoked or regenerated in WordPress admin
- Config file has syntax errors — validate JSON with `jq`

**Fix:**

```bash
cat ~/.elementeer/config.json | jq .
```

If the JSON is valid, generate a new API key under **Settings → Elementeer → API Keys** and update your config. Remember that keys are shown only once upon creation.

## REST API 403 — Insufficient Capability

**Symptom:** The connection works but certain operations fail with 403.

**Diagnosis:** Check which capabilities your key has:

```bash
elementeer-mcp health --json | jq '.api_key.capabilities'
```

**Fix:** The key doesn't have the required capability for the operation you're trying to perform. Generate a new key with expanded capabilities, or edit the existing key's scope under **Settings → Elementeer → API Keys** if key editing is enabled.

!!! tip "Start minimal, add as needed"
    Read-only operations (assessment, listing templates, health checks) need only the
    `site:read` capability. Writing templates requires `templates:write`. See the
    [capability reference](../reference/capabilities.md) for all scopes.

## Connection Refused — Plugin Not Active

**Symptom:** `elementeer-mcp health` fails with "connection refused" or "could not resolve host."

**Diagnosis:**

```bash
curl -I https://your-site.com/wp-json/elementeer/v1/site
```

**Common causes:**

- Elementeer plugin is installed but not activated
- WordPress REST API is disabled (check `.htaccess` or security plugin settings)
- Site is behind a firewall or in maintenance mode
- Pretty permalinks are not enabled

**Fix:** Go to **Plugins → Installed Plugins** and verify Elementeer is active. Go to **Settings → Permalinks** and ensure "Post name" is selected, then click Save Changes to flush rewrite rules. If a security plugin (Wordfence, iThemes Security) is blocking REST access, add `/wp-json/elementeer/` to the allowed paths.

## Elementor Not Detected

**Symptom:** Health check reports `elementor.active: false`.

**Diagnosis:** The health check response will show Elementor status.

**Fix:** Install and activate Elementor (Free or Pro) on your WordPress site. Elementeer requires Elementor's API to function. If Elementor is active but not detected, a plugin conflict may be preventing Elementor's classes from loading — disable other plugins temporarily and re-test.

## MCP Server Port Conflicts

**Symptom:** MCP server logs show `EADDRINUSE` or port-binding errors.

**Diagnosis:** Another process is using the port the MCP server tries to bind to.

**Fix:** Elementeer MCP server uses stdio transport when invoked by AI agents — port conflicts only occur in standalone mode. If you're running in standalone mode, specify an alternative port:

```bash
elementeer-mcp --port 3001
```

For AI agent connections (Claude Desktop, Cursor, OpenCode), the agents handle the stdio transport automatically.

## npm Installation Failures

**Symptom:** `npm install -g @elementeer/mcp` fails with permission errors.

**Fix:**

```bash
# Fix npm global permissions
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
npm install -g @elementeer/mcp

# Add to your shell profile
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
```

Alternatively, use npx instead of global installation:

```bash
npx @elementeer/mcp health
```

## Debug Mode

For deeper diagnostics, enable verbose logging:

```bash
elementeer-mcp --verbose health
```

This outputs the full request/response cycle, including HTTP headers, auth tokens, and response bodies. Use this to identify network-level issues, TLS errors, or unexpected API responses.

If issues persist after following these steps, check the [GitHub issues](https://github.com/elementeer/elementeer-mcp/issues) or the [Elementeer community](https://elementeer.xyz/community).

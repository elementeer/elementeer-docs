# Agent Troubleshooting

Common issues when connecting AI agents to Elementeer, with diagnostic steps and solutions.

## MCP Server Not Starting

**Symptom:** The agent shows "MCP server failed to start" or the tools panel doesn't list Elementeer tools.

**Diagnosis:**

```bash
# Test the server directly
elementeer-mcp health
```

**Common causes:**

- `@elementeer/mcp` is not installed or is an outdated version
- Node.js version is below 20
- Config file path is incorrect in the agent's MCP configuration
- The `npx` command is not found (Node.js not in PATH)

**Fix:** Install or update the MCP server, verify Node.js deployment (`node --version` should show 20+), and validate the agent's MCP config JSON syntax.

## Tool Not Found

**Symptom:** The agent lists tools but Elementeer tools are not among them.

**Diagnosis:** Check if the MCP server started without errors. After restarting the agent, verify the MCP server process is running.

**Common causes:**

- MCP server started but exited due to a config error
- The agent's MCP config points to the wrong command or path
- The MCP server version doesn't match the agent's protocol expectations

**Fix:** Check the agent's MCP server logs. For Claude Desktop, check **Developer Tools** in the app menu. For Cursor, check the MCP server panel. For OpenCode, check the terminal output where OpenCode was launched.

## Connection Refused (Site Down or Blocked)

**Symptom:** `elementeer-mcp health` returns "connection refused" or timeout.

**Diagnosis:**

```bash
curl -I https://your-site.com/wp-json/elementeer/v1/site
```

**Fix:**
- Verify the site URL in `~/.elementeer/config.json` is correct and includes `https://`
- Check that the WordPress site is reachable from your machine
- Ensure no firewall, VPN, or security plugin is blocking REST API access
- Verify the Elementeer plugin is active on the WordPress site

## 401 Unauthorized

**Symptom:** Health check passes but tool calls fail with 401 errors.

**Diagnosis:**

```bash
elementeer-mcp health --verbose
```

**Fix:**
- The API key may have been revoked — generate a new one under **Settings → Elementeer → API Keys**
- The key stored in the MCP server config doesn't match the one in WordPress
- Check for whitespace or copying errors in the key string

## 403 Forbidden — Insufficient Capability

**Symptom:** Some tools work but others return 403.

**Diagnosis:**

```bash
elementeer-mcp health --json | jq '.api_key.capabilities'
```

**Fix:** The API key doesn't have the required capability for the failing operation. Generate a new key with expanded capabilities, or scope an additional key for those specific operations.

## Governance Blocks

**Symptom:** A write operation returns "queued for review" and doesn't execute immediately.

**Diagnosis:** This is expected behavior, not an error. Operations at L2 and L3 governance levels require approval.

**Fix:** Check the WordPress admin under **Settings → Elementeer → Change Queue** to approve or reject queued operations. To avoid queuing for specific operations, you can:
- Use an API key with higher governance trust (if configured)
- Configure auto-approval rules in **Settings → Elementeer → Governance**
- Use L1-level alternatives when available

## Slow Tool Responses

**Symptom:** Tool calls take 5+ seconds to complete.

**Diagnosis:** Check network latency and site performance.

**Fix:**
- Ensure your WordPress site has page caching (WP Rocket, W3 Total Cache, etc.)
- Flush Elementor CSS cache if it's stale
- Check server response times with `curl -w "@curl-format.txt"` 
- Consider increasing the MCP server timeout in `~/.elementeer/config.json`:
  ```json
  { "options": { "timeout": 60000 } }
  ```

## MCP Protocol Version Mismatch

**Symptom:** The agent reports "unsupported protocol version" or the MCP server exits immediately.

**Fix:** Update both the MCP server and the agent to their latest versions. Elementeer v2.2.0 supports the current MCP protocol specification.

## Debug Mode

Enable verbose logging for deeper diagnosis:

```json
// In ~/.elementeer/config.json
{
  "options": {
    "logLevel": "debug"
  }
}
```

Or set the environment variable:

```bash
export ELEMENTEER_LOG_LEVEL=debug
```

This outputs detailed request/response traces including full HTTP headers, tool invocation payloads, and JSON-RPC message flow.

## Getting Help

If issues persist:
- Check [GitHub Issues](https://github.com/elementeer/elementeer-mcp/issues) for known problems
- Review the [Installation Troubleshooting](../install/troubleshooting.md) for plugin and server issues
- Ensure you're running the latest plugin and MCP server versions

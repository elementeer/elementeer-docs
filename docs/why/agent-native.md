# Why Agent-Native WordPress

Elementeer is built on the idea that AI agents should have first-class, structured access to WordPress and Elementor — not through scraping, not through natural language interfaces bolted onto legacy APIs, but through a protocol designed for tool-based AI interaction.

## The MCP Protocol

The **Model Context Protocol** (MCP) is an open standard published by Anthropic for connecting AI agents to external tools and data sources. It defines:

- **Tool discovery** — agents learn available tools at connection time, including parameter types and descriptions
- **Typed invocation** — tools accept JSON Schema-validated inputs and return structured outputs
- **Capability negotiation** — servers declare what they can do; agents decide what to call

Elementeer is a native MCP implementation. Every one of its 128+ tools is a typed, documented, validated MCP tool.

## Why Not REST Alone?

WordPress has a REST API. Elementor has internal PHP APIs. So why add a protocol layer?

### Typed Access

The WordPress REST API returns loosely structured data. Field names vary by plugin. Error formats differ. Schema definitions are inconsistent.

Elementeer's MCP tools each have a Zod schema — a precise, machine-verifiable contract. When an agent calls `elementeer_assess_site`, it knows exactly what parameters to send and exactly what response shape to expect.

### Semantic Understanding

Raw REST APIs expose data. Elementeer exposes operations. An agent doesn't need to know that updating a global color requires a PUT to `/elementor/v1/kit/colors` with a specific payload shape. It calls `elementeer_update_global_colors` with `{"primary": "#6A35FF"}` and Elementeer handles the rest.

### Governance Integration

REST APIs authenticate with keys. Elementeer layers governance on top — L0 reads are instant, L2 writes are queued, L3 changes require consent. This isn't possible with raw REST without building custom middleware.

## Structured Access, Not Scraping

Early AI integrations relied on:

- **DOM scraping** — brittle, breaks on theme updates
- **Natural language to SQL** — dangerous, bypasses WordPress hooks
- **Zapier/IFTTT connectors** — limited to surface-level triggers

Elementeer provides structured, typed, validated access through the WordPress plugin system. It uses Elementor's internal APIs, WordPress hooks, and plugin integrations — the right way to interact with a WordPress site.

## Agent Compatibility

Because Elementeer uses the MCP standard, it works with any MCP-compatible agent:

| Agent | Status |
|-------|--------|
| Claude Desktop | Native MCP support |
| Cursor | MCP support since v0.42 |
| OpenCode | MCP support via configuration |
| Antigravity | MCP support |
| Codex CLI | MCP support |
| Custom agents | Any MCP client can connect |

No custom SDKs. No per-agent integration code. One protocol, all agents.

## The Operational Layer

Elementeer is the operational layer between AI reasoning and WordPress execution. The agent decides what to do; Elementeer provides the tools to do it — safely, quickly, and consistently.

# Vision

Elementeer is the agent-native growth layer for Elementor — a bridge between AI agents and the world's most popular WordPress page builder. Our mission is to make every Elementor site operatorially intelligent.

## The Problem

Elementor powers over 16 million websites. Managing them — templates, global styles, SEO, navigation, performance, integrations — requires clicking through a complex admin interface. It's powerful, but it's manual. As sites grow and portfolios expand, the operational burden compounds.

AI agents can reason, plan, and execute multi-step workflows. But they need structured, typed, validated access to systems. Raw WordPress REST APIs are inconsistent, untyped, and lack the semantic understanding of Elementor's internal model. Elementor's own AI features are embedded in the builder — useful for content generation, not for site operations.

## Our Approach

**Agent-native from the wire up.** Elementeer doesn't retrofit AI onto existing APIs. It exposes the Model Context Protocol — an open standard for tool-based AI interaction — directly to Elementor's internal systems.

Every tool has:

- A typed input schema (Zod-validated)
- A defined capability requirement
- A governance level (L0–L3)
- A deterministic output structure

This means AI agents don't guess. They discover tools, understand parameters, and operate within guardrails.

## The Calm Operator

We believe the best site management happens quietly, in the background, without ceremony. Elementeer is the calm operator — confident, efficient, reliable. No AI hype. No magic. Just well-structured access to the tools you already use.

- **You define what agents can do.** Capabilities and governance are in your control.
- **Agents execute within those boundaries.** They operate at the speed of API calls, not clicks.
- **You review what matters.** L2 and L3 operations are queued for approval.

## Where We're Going

### Phase 1: Agent-Native Foundation (Now)

128 free tools covering the full Elementor site management surface. Template management, site assessment, brand setup, Creator Mode, Theme Builder, SEO, performance, navigation, media, and all 8 integration families. Works with any MCP-compatible agent.

### Phase 2: Operational Power (Advanced Tier)

Advanced agents that manage e-commerce, bookings, translations, and content at scale. Snapshots for safety. Change queues for control. Design tokens for consistency.

### Phase 3: Portfolio Intelligence (Studio Tier)

Multi-site orchestration. Organizational policies. Batch operations across hundreds of sites. A control plane that treats your entire Elementor portfolio as a single operational surface.

## What We're Not

- **Not an AI content generator.** ChatGPT writes copy; Elementeer manages sites.
- **Not a no-code platform replacement.** You still own your WordPress site and Elementor workflow.
- **Not a managed service.** Elementeer runs on your infrastructure — your server, your data, your control.

## The Open-Core Commitment

The MCP server is Apache-2.0. The WordPress plugin is GPL-2.0. The core protocol layer is open. Advanced features fund ongoing development of the free tier. See [Open-Core Model](open-core.md).

Elementeer is the operational layer that makes every Elementor site ready for an AI-native future — on your terms, under your control.

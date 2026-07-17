# Governance Model

Elementeer's governance system ensures that AI agent operations on your WordPress site are safe, intentional, and auditable. Every operation falls into one of four tiers, from instant reads to consent-gated changes.

## The Four Governance Levels

### L0 — Read-Only (Instant)

Operations that only read data and never modify it. These execute immediately without any approval step.

**Examples:** Site assessment, template listing, global style reading, page listing, SEO analysis, performance reporting, health checks, media library browsing.

**Guardrails:** API key capability check only. No audit trail required (though reads are logged for debugging).

### L1 — Safe Writes (Direct)

Operations that modify data but are low-risk, reversible, or non-destructive. These execute directly when the API key has the required capability.

**Examples:** Creating a new template, updating page content, flushing Elementor CSS cache, uploading media, updating navigation menus, modifying global style values.

**Guardrails:** API key capability check + input validation + automatic snapshot creation before the write.

### L2 — Impactful Writes (Auto-Queued)

Operations that have significant scope or potential impact. These are automatically queued for review in the Elementeer admin panel. The site owner can approve or reject them individually.

**Examples:** Deleting templates, bulk page operations, plugin activation/deactivation, user creation, importing large template sets, theme builder modifications.

**Guardrails:** All L1 checks plus automatic queuing. The site owner sees the proposed change, the affected resources, and a diff preview before approving.

### L3 — Consent-Required (High-Risk)

Operations that could materially affect site functionality or security. These require explicit, per-operation consent from the site owner.

**Examples:** Plugin deletion, user deletion, database cleanup operations, deactivating Elementeer itself, changing governance settings.

**Guardrails:** All L2 checks plus a required approval step with a configurable timeout. Unapproved L3 operations expire after 24 hours.

## Change Queue

The **Change Queue** is an Advanced-tier feature that provides a unified review panel for L2 and L3 operations. Site owners can:

- View all queued changes with timestamps and initiating agent
- Preview diffs of proposed content changes
- Approve or reject individual operations
- Approve or reject operations in batches
- Set auto-approval rules for specific operation types from trusted agents

### Queue States

| State | Meaning |
|-------|---------|
| `pending` | Awaiting review |
| `approved` | Approved, awaiting execution |
| `rejected` | Rejected by site owner |
| `expired` | Not reviewed within the timeout period |
| `executed` | Approved and applied |
| `failed` | Approved but execution encountered an error |

## Snapshots

Every L1, L2, and L3 write operation creates a **snapshot** — a point-in-time record of the affected data before the change. Snapshots enable:

- **Instant rollback:** Restore any previous state with one click
- **Diff comparison:** See exactly what changed between two snapshots
- **Audit trail:** Track who (or which agent) made what change and when

```bash
# List snapshots for a page
elementeer-mcp list-snapshots --post-id 42

# Restore to a previous snapshot
elementeer-mcp restore-snapshot --uuid snap_abc123def456
```

Snapshots are stored in the WordPress database as serialized data. The Free tier retains the 10 most recent snapshots per post. Advanced tier supports configurable retention policies and unlimited snapshots.

## Governance Configuration

Site owners configure governance behavior under **Settings → Elementeer → Governance**:

| Setting | Default | Description |
|---------|---------|-------------|
| Auto-approve L1 | On | Execute L1 writes without queuing |
| L2 review timeout | 7 days | How long before queued L2 operations expire |
| L3 consent timeout | 24 hours | How long before L3 consent requests expire |
| Snapshot retention | 10 | Number of snapshots to retain per resource |
| Audit log retention | 90 days | How long to keep operation logs |

## Agent Identity

Every operation is tagged with the originating agent's identity — derived from the API key name. This means you can distinguish operations initiated by "Claude Desktop" from those initiated by "CI Pipeline" in audit logs and the change queue.

## Safety Philosophy

Elementeer's governance model is built on one principle: **reads are free, writes are intentional.** AI agents should be powerful tools for site management, but the site owner always retains control over what changes are applied and when.

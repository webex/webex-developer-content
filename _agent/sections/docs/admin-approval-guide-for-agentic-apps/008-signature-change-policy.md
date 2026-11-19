---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Signature & Change Policy
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

## Signature & Change Policy

### Understanding Tool Signatures

Webex computes a schema signature for each tool and continuously monitors it for changes. When a tool's current signature differs from the version you previously approved, Webex flags it: the tool's behavior may have been modified since your last review.

### When Signatures Change

| Scenario | What Changed | Risk Level | Recommended Action |
|----------|-------------|-----------|-------------------|
| Description update (cosmetic) | Wording improved, no semantic change | Low | Review, re-approve |
| New optional input field | Schema expanded (non-breaking) | Medium | Verify field purpose; re-approve |
| Required field added/removed | Schema breaking change | High | Full re-review required |
| Input validation changed | Constraints tightened or loosened | Medium-High | Assess security impact |
| Tool renamed | Name changed (signature changes) | High | Effectively a new tool; full review |

### Configuring Signature Policy

For each tool, decide on **"Allow signature change"**:

| Setting | When to Use | Trade-off |
|---------|------------|-----------|
| **Off** (recommended for high-security) | Sensitive operations; regulated environments | Users lose access until you re-review; more admin work |
| **On** (acceptable for low-risk) | Read-only tools; trusted publisher with good track record | Reduced admin burden; accepts risk of unreviewed changes |



> **Best Practice**
>
> Default to **Off** for new/unfamiliar servers. Switch to **On** only after establishing trust with the publisher through multiple successful review cycles.



### Runtime Behavior on Signature Drift

When a tool's live signature differs from the stored signature:

| `Allow signature change` | Tool delivered to client SDK? | `unsecure` flag set? |
|--------------------------|------------------------------|----------------------|
| **Off** | No — tool is filtered out of `/listFunctions` results | n/a |
| **On** | Yes — tool is still delivered | **Yes** — `unsecure: true` is included on the tool, so client SDKs and agent UIs can surface a warning to end users |

The `unsecure` flag is your safety net when running with `Allow signature change = On`: clients still receive the tool, but they're alerted that the contract has shifted since you last reviewed it.

---

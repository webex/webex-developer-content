---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Quality Review
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

## Quality Review

### Functional Accuracy

| Check | What to Verify |
|-------|---------------|
| Description matches behavior | Tool does what its description says — no more, no less |
| No hidden functionality | Tool doesn't perform undisclosed actions |
| Predictable behavior | Same inputs produce consistent, expected outputs |
| Error states documented | Known failure modes are described |
| Edge cases handled | Tool behaves gracefully with boundary inputs |

### Error Handling

| Check | What to Verify |
|-------|---------------|
| Structured errors | Errors return machine-readable codes + human-friendly messages |
| No information leakage | Error messages don't expose internal details, stack traces, or secrets |
| Graceful degradation | Tool doesn't crash or hang on invalid input |
| Retry guidance | Errors indicate whether retry is safe (`retryable` flag) |

### Reliability & Performance

| Check | What to Verify |
|-------|---------------|
| Response time | Tools respond within reasonable timeouts |
| Progress streaming | Long operations provide progress feedback |
| Reconnection support | SSE/streaming supports `Last-Event-ID` resume |
| Rate limiting | Server enforces fair-use limits |
| Idempotency | State-changing operations handle retries safely |

### Documentation & Support

| Check | What to Verify |
|-------|---------------|
| Documentation URL | Valid, accessible developer documentation |
| Support channel | Clear path for reporting issues |
| Changelog/versioning | Version history available; deprecation policy stated |
| SLA/uptime | Service level expectations documented |

---

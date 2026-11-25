---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Reliability & Fault Tolerance
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Reliability & Fault Tolerance

### Idempotency & Safe Retries

- **Design all state-changing operations to be idempotent**
- Support `Idempotency-Key` header or JSON-RPC request IDs
- Store pending requests and record completions to detect duplicates
- For truly non-idempotent actions (emails, purchases):
  - Return previous response without re-executing on retry
  - Add human confirmation steps before execution

**Implementation pattern:**
1. Receive request with idempotency key
2. Check if key exists in completion store
3. If exists → return stored response (no re-execution)
4. If not → execute, store result, return response

### Scaling & Failover

- Design for **stateless horizontal scaling** — any node should handle any request
- Store session/task checkpoints in external cache (Redis) or database
- Use session stickiness only for performance optimization, not correctness
- Buffer SSE events in external cache for reconnection support
- Implement health checks and graceful shutdown procedures

### Timeouts, Retries & Backoff

- Implement **timeouts** for all external calls, elicitations, and delegations
- Use **exponential backoff** with jitter for retries
- Return **structured errors** with machine-readable codes AND human-friendly messages
- Distinguish transient errors (retry-safe) from permanent errors (don't retry)

**Error response pattern:**
```json
{
  "error": {
    "code": "UPSTREAM_TIMEOUT",
    "message": "The calendar service did not respond within 30 seconds.",
    "retryable": true,
    "retryAfterSeconds": 5
  }
}
```

### Streaming & Reconnection

- Secure SSE/WebSocket with TLS; validate origins
- Attach **sequence numbers and timestamps** per message frame to prevent replay
- Support `Last-Event-ID` for resuming from last received event
- Enforce **idle timeouts** and heartbeat intervals
- Limit concurrent streams per client to prevent resource exhaustion
- Buffer events for a configurable duration (recommendation: 2–5 minutes)

---

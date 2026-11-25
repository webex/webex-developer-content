---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Observability & Governance
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Observability & Governance

### Structured Logging

- Use structured JSON logs with **correlation IDs** across all requests
- Log every tool invocation with: tool name, sanitized arguments (no secrets), outcome, duration
- Propagate `X-Correlation-Id` headers through all downstream calls
- Redact secrets, tokens, and PII from all log output
- Include timestamps (ISO 8601/UTC), severity levels, and service identifiers

### Metrics & SLOs

Track and emit metrics for:

| Metric | Purpose |
|--------|---------|
| Requests per second (QPS) | Capacity planning |
| Latency (p50, p95, p99) | Performance SLOs |
| Error rate by code | Reliability tracking |
| Progress report frequency | UX quality |
| Queue depth | Backpressure detection |
| Token usage (LLM calls) | Cost visibility |

**Guidelines:**
- Tag metrics by tenant, tool name, and version
- Avoid high-cardinality tags (e.g., don't tag by user ID or request ID)
- Define internal SLOs for performance and cost; track against them
- Use OpenTelemetry for distributed tracing

### Audit Trails

- Maintain **tamper-evident audit logs** with integrity protection
- Log all privileged operations, policy decisions, and consent events
- Store audit entries with secure time sources (NTP-synced)
- Expose events for integration with SIEM and behavioral analytics systems
- Ensure audit logging happens **before** action execution (pre-action logging)

### Versioning & Deprecation

| Rule | Details |
|------|---------|
| Never break published schemas | Existing clients must continue to work |
| Additive changes only | Add optional fields → bump minor version |
| Breaking changes (rare) | Bump major version; keep old version live for several months |
| Deprecation window | Minimum several months with advance communication |
| Version fields | Include schema IDs and version fields in all JSON bodies |
| Deprecation warnings | Surface in annotation fields in response bodies |

---

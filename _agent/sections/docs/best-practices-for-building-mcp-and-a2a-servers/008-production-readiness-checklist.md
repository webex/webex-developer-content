---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Production Readiness Checklist
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Production Readiness Checklist

Before deploying to production, verify:

### Functionality
- [ ] All tool input/output schemas validated with contract tests
- [ ] Idempotency tested (happy path and failure/retry scenarios)
- [ ] Cancellation/abort handling tested
- [ ] Long-running operations stream progress and support resume
- [ ] Elicitation flows work correctly (happy path, timeout, denial)
- [ ] Error responses are structured with codes + friendly messages

### Security
- [ ] All inputs validated against JSON Schema; unknown fields rejected
- [ ] No string concatenation for SQL, shell, or template operations
- [ ] Authorization scopes declared per tool
- [ ] Secrets never logged, never in context, never in outputs
- [ ] PII redacted from all logs and telemetry
- [ ] Data encrypted at rest (KMS) and in transit (TLS)
- [ ] Supply chain: dependencies pinned, scanned, SBOM generated
- [ ] Network: outbound restricted, SSRF prevented, certificates pinned
- [ ] Security review completed and documented

### Reliability
- [ ] Streaming and reconnection tested (SSE drop/reconnect via Last-Event-ID)
- [ ] Timeouts configured for all external calls
- [ ] Exponential backoff with jitter for retries
- [ ] Graceful degradation under load verified
- [ ] Chaos tests passed (worker crash, proxy timeout, connection break)
- [ ] Health checks and graceful shutdown implemented

### Observability
- [ ] Structured logging with correlation IDs in place
- [ ] Metrics emitted: QPS, latency, error rates, queue depth
- [ ] SLOs defined and dashboards created
- [ ] Audit trails implemented for privileged operations
- [ ] Runbooks documented for common failure scenarios
- [ ] Alerting configured for SLO violations

### Governance
- [ ] Tool specifications match actual runtime behavior
- [ ] Friendly descriptions, tags, and documentation URLs provided
- [ ] Rate limits defined (per-user, per-client, per-tenant)
- [ ] Versioning strategy documented
- [ ] Deprecation policy in place for future changes

---

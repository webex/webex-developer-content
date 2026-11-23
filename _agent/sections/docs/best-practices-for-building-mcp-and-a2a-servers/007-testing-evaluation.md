---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Testing & Evaluation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Testing & Evaluation

### Required Test Categories

| Category | What to Test |
|----------|-------------|
| **Contract tests** | Schema validation, required fields, error codes, idempotency behavior |
| **Integration tests** | End-to-end with real (or realistic mock) dependencies |
| **AI evaluations** | Typical prompts → verify correct tool selection and argument population |
| **Security tests** | Input injection, auth bypass, privilege escalation, SSRF |
| **Load/performance** | QPS, latency, memory under streaming, SSE reconnection |
| **Chaos tests** | Worker crash, connection drop, proxy timeout, partial failure |
| **Regression gates** | Re-run evaluations when underlying LLM models change |

### AI Evaluation Guidelines

- Create evaluation suites with representative prompts and expected tool selections
- Test that LLMs correctly populate required fields from conversation context
- Use tolerances and snapshots to distinguish acceptable variation from regression
- Re-evaluate periodically even without changes — model behavior can drift
- Test edge cases: ambiguous prompts, conflicting tools, missing required info

### Load & Cost Testing

- Benchmark with SSE enabled to capture streaming-specific performance
- Measure memory usage, QPS capacity, and perceived latency (time-to-first-byte)
- Track LLM token usage per operation — monitor for unexpected cost increases
- Validate graceful degradation under load (backpressure, admission control)

---

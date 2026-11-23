---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Table of Contents
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Table of Contents

- [Designing Your Tools & Skills](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#designing-your-tools--skills)
  - [Granularity](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#granularity)
  - [Naming Conventions](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#naming-conventions)
  - [Input & Output Schemas](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#input--output-schemas)
  - [Resources vs. Tools](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#resources-vs-tools)
- [Long-Running Operations](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#long-running-operations)
  - [Progress & Status Reporting](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#progress--status-reporting)
  - [Elicitation (Human-in-the-Loop)](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#elicitation-human-in-the-loop)
  - [Delegation & Sampling](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#delegation--sampling)
  - [Operation Artifacts](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#operation-artifacts)
- [Security & Privacy](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#security--privacy)
  - [Input Validation & Sanitization](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#input-validation--sanitization)
  - [Authorization & Scopes](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#authorization--scopes)
  - [Secrets Management](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#secrets-management)
  - [Data Handling & Privacy](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#data-handling--privacy)
  - [Supply Chain Security](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#supply-chain-security)
  - [Network Security](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#network-security)
  - [Injection & Manipulation Defenses](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#injection--manipulation-defenses)
- [Reliability & Fault Tolerance](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#reliability--fault-tolerance)
  - [Idempotency & Safe Retries](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#idempotency--safe-retries)
  - [Scaling & Failover](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#scaling--failover)
  - [Timeouts, Retries & Backoff](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#timeouts-retries--backoff)
  - [Streaming & Reconnection](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#streaming--reconnection)
- [Observability & Governance](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#observability--governance)
  - [Structured Logging](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#structured-logging)
  - [Metrics & SLOs](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#metrics--slos)
  - [Audit Trails](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#audit-trails)
  - [Versioning & Deprecation](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#versioning--deprecation)
- [Testing & Evaluation](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#testing--evaluation)
- [Production Readiness Checklist](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers#production-readiness-checklist)

---

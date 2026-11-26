---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-rate-limits
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Configuration APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-rate-limits). [Full Markdown](../../../../docs/webex-connect-rate-limits.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [When a limit is exceeded](002-when-a-limit-is-exceeded.md)

## Article introduction

Webex Connect applies rate limits across its API families to protect service availability and provide predictable performance. The applicable limit depends on the API family, operation, and limits configured for your organization.

## Selected section

## Configuration APIs

Configuration APIs use limits defined for each API family and operation. These limits are evaluated independently of Messaging API throughput.

### Digital Channel Onboarding APIs

Rate limits apply to operations that create, retrieve, or update digital channel assets. The API Reference is authoritative for the limit that applies to each operation, including its evaluation scope and time window.

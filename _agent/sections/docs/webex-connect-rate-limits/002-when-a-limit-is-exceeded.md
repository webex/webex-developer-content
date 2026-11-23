---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-rate-limits
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- When a limit is exceeded
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-rate-limits). [Full Markdown](../../../../docs/webex-connect-rate-limits.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex Connect applies rate limits across its API families to protect service availability and provide predictable performance. The applicable limit depends on the API family, operation, and limits configured for your organization.

## Selected section

## When a limit is exceeded

Reduce the request rate and follow the rate-limit handling documented for the API family.

Do not retry rate-limited Digital Channel Onboarding API requests. Verify the current state of the asset before performing any further operation.

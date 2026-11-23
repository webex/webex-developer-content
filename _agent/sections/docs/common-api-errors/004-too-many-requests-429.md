---
type: Excerpt
canonical_url: https://developer.webex.com/docs/common-api-errors
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Too Many Requests (429)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/common-api-errors). [Full Markdown](../../../../docs/common-api-errors.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Invalid Authorization header (400)](001-invalid-authorization-header-400.md)

## Article introduction

Our APIs return standard HTTP status codes for request responses. If an error occurs, more information will be provided in the response.

## Selected section

## Too Many Requests (429)

Too many requests have been sent in a given amount of time so the request has been rate limited. The request has a valid token and has not been processed. The 429 response will have proper CORS headers, but will not have a body.

See [Rate Limiting](https://developer.webex.com/docs/rate-limiting) for details.

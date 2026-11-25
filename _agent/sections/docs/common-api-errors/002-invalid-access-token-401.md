---
type: Excerpt
canonical_url: https://developer.webex.com/docs/common-api-errors
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Invalid Access Token (401)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/common-api-errors). [Full Markdown](../../../../docs/common-api-errors.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Invalid Authorization header (400)](001-invalid-authorization-header-400.md)

## Article introduction

Our APIs return standard HTTP status codes for request responses. If an error occurs, more information will be provided in the response.

## Selected section

## Invalid Access Token (401)

The token provided in Authorization header must be valid (unaltered) and unexpired.  Else, you will get `401 Unauthorized` response and the request will not be processed. See [Authentication](https://developer.webex.com/docs/authentication) for how to get a token.

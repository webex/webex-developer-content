---
type: Excerpt
canonical_url: https://developer.webex.com/docs/common-api-errors
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Operation is Forbidden (403)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/common-api-errors). [Full Markdown](../../../../docs/common-api-errors.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Invalid Authorization header (400)](001-invalid-authorization-header-400.md)

## Article introduction

Our APIs return standard HTTP status codes for request responses. If an error occurs, more information will be provided in the response.

## Selected section

## Operation is Forbidden (403)

All API requests require a variety of scopes. In order to interact with a given API, a user's token needs to have the correct scope, or else they will be forbidden from interacting with the API.

Additionally, some APIs require the user to have an administrator role.

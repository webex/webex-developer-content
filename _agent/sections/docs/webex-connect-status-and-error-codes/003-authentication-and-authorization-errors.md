---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-status-and-error-codes
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication and authorization errors
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-status-and-error-codes). [Full Markdown](../../../../docs/webex-connect-status-and-error-codes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex Connect APIs use HTTP status codes and response bodies to communicate the outcome of a request.

## Selected section

## Authentication and authorization errors

For `401 Unauthorized`, verify that the request includes the authentication credentials required by the API and that they are valid and current. For APIs that use bearer-token authentication, verify this header:

```http
Authorization: Bearer <access-token>
```

For `403 Forbidden`, verify the required scope, the user's organization access, and permission to perform the requested operation. A valid token alone is not sufficient.

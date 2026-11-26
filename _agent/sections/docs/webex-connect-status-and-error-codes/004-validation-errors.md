---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-status-and-error-codes
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Validation errors
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-status-and-error-codes). [Full Markdown](../../../../docs/webex-connect-status-and-error-codes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and authorization errors](003-authentication-and-authorization-errors.md)

## Article introduction

Webex Connect APIs use HTTP status codes and response bodies to communicate the outcome of a request.

## Selected section

## Validation errors

For `400 Bad Request`, check the operation definition for:

- required query parameters and headers;
- valid identifiers and values;
- required request body fields; and
- API-specific configuration objects.

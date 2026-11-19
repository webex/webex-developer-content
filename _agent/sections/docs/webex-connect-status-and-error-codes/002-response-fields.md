---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-status-and-error-codes
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Response fields
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-status-and-error-codes). [Full Markdown](../../../../docs/webex-connect-status-and-error-codes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and authorization errors](003-authentication-and-authorization-errors.md)

## Article introduction

Webex Connect APIs use HTTP status codes and response bodies to communicate the outcome of a request.

## Selected section

## Response fields

API responses can include these common fields:

| Field | Description |
|---|---|
| `code` | API result or error code. |
| `description` | Human-readable result or error description. |
| `transid` | Transaction identifier used to trace the request. |

Additional response fields vary by API and operation. See the API Reference for the response schema supported by each operation.

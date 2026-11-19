---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-status-and-error-codes
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- HTTP status codes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-status-and-error-codes). [Full Markdown](../../../../docs/webex-connect-status-and-error-codes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and authorization errors](003-authentication-and-authorization-errors.md)

## Article introduction

Webex Connect APIs use HTTP status codes and response bodies to communicate the outcome of a request.

## Selected section

## HTTP status codes

| Status | Meaning |
|---|---|
| `200 OK` | The request was completed successfully. |
| `400 Bad Request` | A required query parameter, header, or body field is missing or invalid. |
| `401 Unauthorized` | The bearer token is missing, invalid, or expired. |
| `403 Forbidden` | The user does not have access to the organization or permission to perform the requested operation. |
| `500 Internal Server Error` | Webex Connect could not complete the operation because of an internal error. |

The API Reference for each operation is authoritative for the response codes and schemas it supports.

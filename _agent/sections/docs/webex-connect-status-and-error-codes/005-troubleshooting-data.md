---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-status-and-error-codes
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting data
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-status-and-error-codes). [Full Markdown](../../../../docs/webex-connect-status-and-error-codes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and authorization errors](003-authentication-and-authorization-errors.md)

## Article introduction

Webex Connect APIs use HTTP status codes and response bodies to communicate the outcome of a request.

## Selected section

## Troubleshooting data

Record the HTTP status, `code`, `description`, `transid`, timestamp, operation, and organization ID. If you supplied a `trackingid` request header, record that value too. Never log or share personal access tokens, client secrets, credentials, or other sensitive configuration data.

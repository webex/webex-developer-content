---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server). [Full Markdown](../../../../docs/contact-center-operation-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Scopes](005-scopes.md)

## Selected section

## Authentication

**Auth Type:** OAuth 2.0 Bearer Token

**Issuer:** `https://idbroker.webex.com`

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server validates organization access and forwards the token to Webex Contact Center APIs on behalf of the authenticated user.

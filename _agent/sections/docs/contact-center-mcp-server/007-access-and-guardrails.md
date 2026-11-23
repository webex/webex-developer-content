---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Access and Guardrails
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server). [Full Markdown](../../../../docs/contact-center-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](005-authentication.md) [Scopes](006-scopes.md)

## Selected section

## Access and Guardrails

- Users must have access to the target Webex Contact Center organization.
- Read tools require configuration read permission. Write tools require configuration write permission and a user account context.
- The server validates `orgId` for every tool call because organization ID is supplied as a tool argument.
- The server applies guardrails for per-organization/per-tool rate limits, write payload size, maximum nodes, maximum edges, and downstream service failures.
- Write tools validate and normalize FlowV2 before saving. A flow should be validated before any publish or production lifecycle action outside this MCP tool surface.

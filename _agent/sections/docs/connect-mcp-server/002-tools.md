---
type: Excerpt
canonical_url: https://developer.webex.com/docs/connect-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/connect-mcp-server). [Full Markdown](../../../../docs/connect-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

## Tools

3 tools covering sender discovery and outbound SMS and email messaging:

| Tool | Description |
|------|-------------|
| `webex-sender-ids` | Returns sender IDs that the administrator has enabled for AI Agent Messaging. Results can be filtered by channel and use case so the agent selects an approved sender before sending. |
| `webex-sms-message` | Sends a non-templated SMS using an approved sender ID. The recipient must be in E.164 format, and the message body must not exceed 1,024 characters. Use `contentType` `text` for GSM 03.38 characters and `unicode` when the message contains characters outside GSM 03.38. |
| `webex-email-message` | Sends a non-templated plain-text or HTML email using an approved sender ID. Supports attachments. The body must not exceed 500,000 characters, and the total message size must not exceed 25 MB. |

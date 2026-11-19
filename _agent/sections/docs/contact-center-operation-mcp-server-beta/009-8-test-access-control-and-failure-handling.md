---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 8. Test access control and failure handling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 8. Test access control and failure handling

Use administrator-approved test accounts or test conditions:

- A user without Contact Center access attempts a read-only check.
- A user with limited permissions attempts to read an unavailable resource.
- An invalid flow, object, contact, agent, session, or task ID is supplied.
- A report uses an invalid or reversed time range.
- A Search query uses an unsupported field or record type.
- An authorization expires or is revoked.

Expected behavior:

- The request fails clearly and safely.
- No unauthorized data is returned.
- No write occurs.
- The message explains the next action, such as correcting the input or requesting access.
- The error does not expose tokens, secrets, or unrelated customer data.

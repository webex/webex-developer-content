---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 5. Test real-time subscriptions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center MCP Server](https://developer.webex.com/docs/contact-center-mcp-server).

## Selected section

## 5. Test real-time subscriptions

1. Use `wxcc-realtime` to discover supported event types.
2. Use `wxcc-realtime` to list existing webhook subscriptions.
3. Use `wxcc-realtime` to create and update a test webhook subscription.
4. Use `wxcc-realtime` to provision a WebSocket session when the client supports it and confirm the response includes a `webSocketUrl` and `subscriptionId`.
5. Use `wxcc-realtime` to delete the test webhook subscription after validation.

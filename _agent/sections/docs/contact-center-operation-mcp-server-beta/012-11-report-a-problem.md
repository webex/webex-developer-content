---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 11. Report a problem
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 11. Report a problem

Stop and report the issue when:

- The server cannot connect after the administrator confirms setup.
- A read-only tool returns data outside the target organization.
- A read-only tool changes configuration or operational data.
- A permitted request fails unexpectedly.
- An unauthorized request succeeds.
- A report gives a result that cannot be explained using the same time range, filters, and data level.
- A recording check exposes media instead of approved metadata.
- A Virtual Agent or AI Agent result exposes information outside the approved test.

Include the tool name, date and time with time zone, region, user role, expected result, actual result, sanitized error message, and test object ID if one was used. Do not send access tokens, refresh tokens, recording URLs, transcripts, or unnecessary customer information.

To share feedback, ask questions, or report issues, use the beta feedback channel shared with your beta invitation or Cisco beta contact.

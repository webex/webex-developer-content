---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Cleanup and rollback
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center MCP Server](https://developer.webex.com/docs/contact-center-mcp-server).

## Selected section

## Cleanup and rollback

- Do not publish or production-bind the `MCP_TEST_<date>` flow draft.
- Delete test entry points, business hours, dial plans, dial numbers, and webhook subscriptions after validation.
- If a test produces an unexpected write or exposes data outside the target organization, stop testing and report the flow or resource ID, tool name, and error without sharing tokens or customer data.

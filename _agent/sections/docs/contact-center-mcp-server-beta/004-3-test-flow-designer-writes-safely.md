---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 3. Test Flow Designer writes safely
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center MCP Server](https://developer.webex.com/docs/contact-center-mcp-server).

## Selected section

## 3. Test Flow Designer writes safely

1. Use `wxcc-get-flow-template` to retrieve a starter FlowV2 template.
2. Use `wxcc-create-flow` to create an unpublished draft named `MCP_TEST_<date>`.
3. Use `wxcc-save-flow-draft` or `wxcc-patch-flow-draft` to make a small change.
4. Use `wxcc-validate-flow` and confirm validation succeeds before any publish or production action.

Keep the test flow unpublished and do not bind it to a production entry point. Record its name and ID for administrator cleanup.

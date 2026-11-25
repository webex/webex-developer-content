---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the result
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Verify the result

A statement from the agent that it posted a message is not sufficient. Check all of the following:

- The tool history shows one successful message creation for the approved destination and text.
- A subsequent message lookup returns the same message ID, destination, and text, including your unique marker.
- The message is visible in the intended test space in the Webex app.

Webex uses `roomId` to identify the destination and `id` to identify a message in its REST API. See [Create a Message](https://developer.webex.com/docs/api/v1/messages/create-a-message) and [Get Message Details](https://developer.webex.com/docs/api/v1/messages/get-message-details) for the underlying API contracts. Inspect your MCP tool's actual result format rather than assuming it is identical to the REST response.

If the write times out or its result is unclear, inspect the test space and available read results before considering another attempt. Do not repeat a create operation merely because the agent did not receive a success response. If a duplicate exists, record the failed check and review what was retried.

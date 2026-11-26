---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Inspect the destination
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Inspect the destination

In the prompts, replace `YOUR_TEST_SPACE_TITLE` with the exact name of your test space. After the first lookup, replace `YOUR_TEST_ROOM_ID` with the returned identifier. These are input placeholders, not values to send unchanged.

```text
Use only the Webex Messaging MCP Server's read tools.
Find the group space with the exact title YOUR_TEST_SPACE_TITLE.
Show its title and room ID from the tool result.
If there are no matches or more than one match, stop and ask me to identify
the intended space. If the available results are incomplete, ask me for the
exact room ID instead of assuming a unique match.
Do not create, change, or delete anything.
```

Inspect the tool call and its returned data. Confirm the destination against the test space in the Webex app, then keep its room ID for the remaining steps. Matching titles alone are insufficient when several spaces share a name. If the agent cannot resolve one destination, do not continue to a write.

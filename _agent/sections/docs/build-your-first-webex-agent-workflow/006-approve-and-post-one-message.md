---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Approve and post one message
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Approve and post one message

For the posting attempt, request a fresh draft with a new marker. Enable `webex-create-message` for this session while retaining its manual approval requirement. Keep the two read tools available.

After reviewing the new draft, give the agent this instruction:

```text
Post exactly the draft I just approved to room ID YOUR_TEST_ROOM_ID.
Use webex-create-message from the Webex Messaging MCP Server once.
Do not change the text, use another destination, add mentions or attachments,
or retry automatically if the result is uncertain.
After a successful creation, use webex-get-message to retrieve that message
by the identifier returned by the creation tool.
Report the message ID, room ID, text, and creation time from the returned data.
If creation or verification fails, report the observed result without claiming
that the message was posted or verified.
```

Before approving the client's write-tool confirmation, inspect its destination and complete text. Reject the call if either differs from the approved draft. If the client offers no confirmation, stop and correct the tool's approval configuration before attempting a write.

You can also reject the write confirmation to exercise the approval boundary. Confirm that the rejected attempt produces no new message before starting another attempt with a new marker.

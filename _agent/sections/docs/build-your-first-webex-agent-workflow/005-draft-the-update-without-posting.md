---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Draft the update without posting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Draft the update without posting

Use the supplied facts below. No production conversation or customer data is needed.

```text
Prepare a short plain-text update for test space YOUR_TEST_ROOM_ID.
Use only these synthetic facts:
- The demo integration connected successfully.
- The read-only space lookup passed.
- The next step is to test one approved message.

Prefix the draft with a unique marker I can search for:
AGENT-LAB-YOUR_UNIQUE_RUN_LABEL

Show the complete message and destination room ID. Do not post it.
Do not add recipients, mentions, attachments, or facts I did not provide.
Wait for my explicit approval of the final text and destination.
```

Replace `YOUR_UNIQUE_RUN_LABEL` with a label unique to this attempt. Review the draft for all three facts, the intended room ID, and the absence of invented details.

To test withholding approval, reply:

```text
Do not post this draft. Cancel this attempt and make no changes in Webex.
```

Check the tool history and the test space. This attempt should contain no message-creation call or new message with its marker. If you find a write, stop the exercise and review the client's available tools and approval settings.

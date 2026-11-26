---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect the client and set approvals
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Connect the client and set approvals

1. Open the [Messaging MCP Server guide](https://developer.webex.com/docs/messaging-mcp-server) and copy its server URL.
2. Follow the token-based setup in [Connect VS Code to a Webex MCP server](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode), using the Messaging server URL. Generate and enter the token through the documented setup flow, rather than asking the agent to handle it.
3. Start the server and confirm that its tools are available in your Copilot session. Inspect the current tool descriptions and input schemas before using them; the prompts below express the task rather than hard-coding a tool-call payload.
4. Initially expose only `webex-get-space` and `webex-get-message` from this server to the session. Keep unrelated tools unavailable for this exercise.
5. Use manual tool approvals. Before enabling `webex-create-message`, configure it to require confirmation and remove any saved pre-approval for that tool. Follow [VS Code's tool approval guidance](https://code.visualstudio.com/docs/agents/run/approvals#tool-approval). Do not use a mode that approves every call automatically.

The instruction to wait for approval is part of this workflow. Keep the client's write-approval control enabled as well.

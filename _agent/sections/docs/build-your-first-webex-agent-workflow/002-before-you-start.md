---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you start
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Before you start

You need:

- VS Code with GitHub Copilot and a session that can use MCP tools. Organization policy must permit the connection.
- A Webex account that can access and post in a dedicated test space. Use a space whose members have agreed to receive tutorial messages.
- Administrator enablement of the [Messaging MCP Server](https://developer.webex.com/docs/messaging-mcp-server), access for your user, and the three tools listed below. Follow [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) if administrator setup is needed.

Use only synthetic content. Keep credentials out of prompts, screenshots, source files, and chat transcripts.

### Tools and scopes

This workflow uses these capabilities from the Messaging MCP Server:

| Tool | Purpose | Tool scope |
| --- | --- | --- |
| `webex-get-space` | Inspect the destination space. | `spark:rooms_read` |
| `webex-create-message` | Post the approved plain-text update. | `spark:messages_write` |
| `webex-get-message` | Retrieve the posted message for verification. | `spark:messages_read` |

`spark:mcp` is also required for the server connection. A Webex Client Identity Token (WCIT) starts with that connection scope; supported clients use MCP elicitation to request additional tool scopes at runtime. Follow the [Webex MCP authentication guide](https://developer.webex.com/docs/webex-agentic-mcp-servers#authentication) for the authentication method your client supports.

Scope consent, administrator enablement, and your account's access to a space are separate requirements. A connection alone does not establish permission to post.

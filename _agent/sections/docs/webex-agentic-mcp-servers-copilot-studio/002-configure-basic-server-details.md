---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure Basic Server Details
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-copilot-studio.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This guide walks you through how you can connect your agent in Copilot Studio to Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Selected section

## Configure Basic Server Details

1. Go to the **Tools** page for your agent
2. Select **Add a tool**
3. Select **New tool**
4. Select **Model Context Protocol**. The MCP onboarding wizard appears.
5. Fill in the required fields: **Server name**, **Server description**, and **Server URL**
6. Select the authentication type for the MCP server as **OAuth 2.0**
7. Select **Manual** as the OAuth 2.0 type. More fields will appear for you to configure the OAuth 2.0 settings.

> Make sure to write a brief, but clear description of what your MCP server does. The agent orchestrator uses this information to identify whether to call your server at runtime.

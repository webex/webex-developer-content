---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ai-in-webex
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect External MCP Servers to Webex AI
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ai-in-webex). [Full Markdown](../../../../docs/ai-in-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn how Webex supports agentic AI, where Model Context Protocol (MCP) fits, and which connection model to use for your first Webex AI project.

## Selected section

## Connect External MCP Servers to Webex AI

Choose this path when the Webex AI Agent handling a live customer conversation in Webex Contact Center needs data or an action from a third-party system.

For example, the Webex AI Agent could use an order-processing MCP server to:

- Retrieve the customer's order details and current status.
- Check fulfillment or shipping information.
- Submit an approved order action when the MCP tool supports it.
- Use the result to continue the customer conversation.

In this pattern, the external MCP server does not bring its own agent into Webex Contact Center. It exposes bounded tools to the Webex AI Agent. Developers define those tools, and administrators decide which servers and tools the organization can use.

Start by learning how to [configure an MCP client action in Webex AI Agent Studio](https://developer.webex.com/docs/mcp-ai-agent-studio). To make a server available through the Webex agentic platform, review [Agentic Apps concepts](https://developer.webex.com/docs/agentic-apps-overview) and [onboard your MCP server](https://developer.webex.com/docs/onboard-your-mcp-server).

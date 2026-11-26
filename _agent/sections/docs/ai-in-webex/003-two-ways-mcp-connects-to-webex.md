---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ai-in-webex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Two ways MCP connects to Webex
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ai-in-webex). [Full Markdown](../../../../docs/ai-in-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn how Webex supports agentic AI, where Model Context Protocol (MCP) fits, and which connection model to use for your first Webex AI project.

## Selected section

## Two ways MCP connects to Webex

People often call these patterns “inbound MCP” and “outbound MCP,” but those labels change depending on where you stand. The Webex Developer Portal names the two paths **Connect Webex MCP Servers to External Clients** and **Connect External MCP Servers to Webex AI**.

![Two MCP paths: an external AI agent uses Webex tools, while a caller reaches a Webex Contact Center AI Agent that uses an external MCP server to access an external business system. Order processing is shown as one example.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt51314f0dafcb892a/6a8c64e8bcc5de9573d39c69/ai-in-webex-mcp-directions-themed.png)





> **Connect Webex MCP Servers to External Clients**
>
> <p><strong>The agent lives in the external AI application used by an end user or administrator.</strong></p>
> <p>That external agent is the MCP client. It connects to a Webex MCP server, discovers approved tools, and uses those tools to work with Webex services on behalf of the authenticated user.</p>
> <p><strong>Direction:</strong> External AI agent → Webex MCP server → Webex services</p>






> **Connect External MCP Servers to Webex AI**
>
> <p><strong>The agent is the Webex AI Agent handling a customer conversation in Webex Contact Center.</strong></p>
> <p>A caller or customer contacts Webex Contact Center. During the live conversation, the Webex AI Agent acts as the MCP client and can call approved tools from an external MCP server, such as a server for an order processing system.</p>
> <p><strong>Direction:</strong> Caller or customer → Webex Contact Center AI Agent → external MCP server → external business system</p>





### Where the agent lives

| Pattern | Person starts in | Agent and MCP client live in | MCP server exposes | Destination |
|---------|------------------|------------------------------|--------------------|-------------|
| Connect Webex MCP Servers to External Clients | An external AI application | The external AI application | Approved Webex tools | Webex services |
| Connect External MCP Servers to Webex AI | A customer conversation with Webex Contact Center | Webex AI Agent in Webex Contact Center | Approved tools for a third-party service | An external business system, such as an order processing system |

Tool requests move toward the destination shown in the chart. Results return to the agent through the same connection.

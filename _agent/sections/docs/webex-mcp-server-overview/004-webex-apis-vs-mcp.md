---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-mcp-server-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex APIs vs MCP
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-mcp-server-overview). [Full Markdown](../../../../docs/webex-mcp-server-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Webex APIs vs MCP

Webex APIs are REST-based HTTP endpoints provided by Cisco Webex that developers call directly from their applications to integrate collaboration features like messaging, meetings, calling and device control. You make standard HTTP requests with authentication tokens to interact with Webex services.

### When to Use Webex APIs

Choose Webex REST APIs when you need:

- **Full Control** — Precise control over every API call and response
- **Performance** — Direct API calls with minimal latency
- **Complex Logic** — Your application has intricate business logic
- **Webhooks** — Real-time event notifications via webhooks
- **Enterprise Applications** — Large-scale solutions that need direct API access for performance and security compliance

**Example use cases:**
- Building a custom collaboration app
- Automated meeting scheduling system
- Enterprise SSO integration
- Real-time presence monitoring dashboard

### When to Use Webex MCP

Choose Webex MCP when you need:

- **AI Integration** — Enable AI agents and LLM platforms to interact with Webex using natural language
- **Rapid Prototyping** — Get started quickly without writing repetitive API integration code
- **Cross-Platform** — Connect Webex to any MCP-compatible AI client with a single configuration

**Example use cases:**
- AI assistant that manages your Webex communications
- Chatbot that schedules meetings and takes notes
- Natural language interface for searching messages and spaces

### Using Both Together

You can combine both approaches. For example:

1. Use Webex APIs for direct, programmatic control and production applications
2. Use MCP to enable AI assistants to interact with Webex through natural language

The choice depends on your use case, technical requirements, and whether AI-powered interactions are central to your application.

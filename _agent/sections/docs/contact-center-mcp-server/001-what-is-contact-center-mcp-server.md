---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What is Contact Center MCP Server?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server). [Full Markdown](../../../../docs/contact-center-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](005-authentication.md) [Scopes](006-scopes.md)

## Selected section

## What is Contact Center MCP Server?

The Webex Contact Center MCP Server enables AI agents and automation tools to securely interact with Webex Contact Center capabilities on behalf of authenticated users.

It supports Day 0 administration and Flow Designer operations, including creating, updating, and deleting entry points, business hours, dial plans, and dial numbers; reviewing read-only configuration for queues and teams; searching and managing flows; creating and updating drafts; modifying nodes and edges; and validating flow definitions.

The server also provides AI-generated customer context by alias, including concise summaries, insights, and frequently discussed topics, without exposing transcripts, prompts, or internal evidence. Real-time capabilities enable agents to manage webhook subscriptions for telemetry events and provision WebSocket sessions for use cases such as live wallboards and supervisor dashboards.

Administrators enable and govern the server through the Webex Agentic Platform or the Agentic Apps settings in Control Hub.

The current flow authoring contract is FlowV2, and activity discovery uses ActivityV2, a condensed schema designed for API and LLM clients.

> **Prerequisites:** Administrators must enable the Webex Contact Center MCP Server for the organization through Webex Agentic Platform / Control Hub Agentic Apps settings before users can connect supported MCP clients. Administrators can also control which Contact Center MCP tools are enabled for the organization, including the Flow Designer tools listed below.



> MCP server availability and your organization's endpoint require sign-in on the [official portal page](<https://developer.webex.com/docs/contact-center-mcp-server>).

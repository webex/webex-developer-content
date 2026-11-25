---
type: Excerpt
canonical_url: https://developer.webex.com/docs/security-overview
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect Only to Trusted Servers
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/security-overview). [Full Markdown](../../../../docs/security-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Publish](003-before-you-publish.md)

## Article introduction

MCP servers allow AI agents and applications to connect with external tools, services, and data sources. Because these servers can expose tools that read data, send data, or take actions on behalf of a user or organization, it is important to connect only to MCP servers that you know and trust. Use this guide to understand what to review before connecting to an MCP server, and what to consider when building or publishing your own MCP server.

## Selected section

## Connect Only to Trusted Servers

Whenever possible, use official MCP servers hosted by the service provider. For example, use Stripe's official MCP server at [mcp.stripe.com](https://mcp.stripe.com) instead of an unofficial Stripe MCP server hosted by a third party.

If an official MCP server is not available, you may choose to use a server hosted by another organization that proxies requests to the service through an API. Before connecting, review how that organization handles your data, what systems it connects to, and whether you trust the server operator.

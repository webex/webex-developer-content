---
type: Guide
title: Security Overview
display_title: Security Overview
canonical_url: https://developer.webex.com/docs/security-overview
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/security-overview)

MCP servers allow AI agents and applications to connect with external tools, services, and data sources. Because these servers can expose tools that read data, send data, or take actions on behalf of a user or organization, it is important to connect only to MCP servers that you know and trust. Use this guide to understand what to review before connecting to an MCP server, and what to consider when building or publishing your own MCP server.

## Connect Only to Trusted Servers

Whenever possible, use official MCP servers hosted by the service provider. For example, use Stripe's official MCP server at [mcp.stripe.com](https://mcp.stripe.com) instead of an unofficial Stripe MCP server hosted by a third party.

If an official MCP server is not available, you may choose to use a server hosted by another organization that proxies requests to the service through an API. Before connecting, review how that organization handles your data, what systems it connects to, and whether you trust the server operator.

## Review What the Server Can Do

Before connecting to an MCP server, review the tools it exposes and the actions those tools can perform. Some tools may only return read-only information, while others may create, update, delete, send, or publish data.

Check whether the server can:

- Access user or organization data
- Send messages, emails, or notifications
- Create, update, or delete records
- Retrieve sensitive or regulated information
- Perform actions in connected third-party services
- Store or process data outside Webex

Only connect if the server's capabilities match your intended use case.

## Before You Publish

Before publishing or sharing an MCP server, review:

- Tool names, descriptions, and expected behavior
- Required authentication and scopes
- Data accessed, processed, stored, or transmitted
- Error handling and logging behavior
- Tenant or organization isolation
- Rate limits and abuse prevention
- Compliance and security review requirements
- Support ownership and escalation path

## Recommended Checklist

Before connecting to an MCP server, ask:

- Is this server hosted by the official service provider?
- If not, do I trust the organization hosting it?
- Do I understand what tools the server exposes?
- Are the requested permissions appropriate?
- Could this server access or store sensitive data?
- Is the server intended for production use?
- Do I know who owns and supports this server?

If the answer to any of these is unclear, review further before connecting.

## Build Responsibly

If you are building an MCP server, design it with transparency and safety in mind. Clearly describe each tool, request only the permissions needed, avoid exposing unnecessary data, and make sure users understand what actions the server can perform.

Do not include malicious, misleading, or hidden behavior in tool definitions. A trusted MCP ecosystem depends on clear ownership, safe defaults, and responsible handling of user and organization data.

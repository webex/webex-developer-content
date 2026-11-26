---
type: Excerpt
canonical_url: https://developer.webex.com/docs/security-overview
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Review What the Server Can Do
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/security-overview). [Full Markdown](../../../../docs/security-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Publish](003-before-you-publish.md)

## Article introduction

MCP servers allow AI agents and applications to connect with external tools, services, and data sources. Because these servers can expose tools that read data, send data, or take actions on behalf of a user or organization, it is important to connect only to MCP servers that you know and trust. Use this guide to understand what to review before connecting to an MCP server, and what to consider when building or publishing your own MCP server.

## Selected section

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

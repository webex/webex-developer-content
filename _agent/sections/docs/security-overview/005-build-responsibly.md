---
type: Excerpt
canonical_url: https://developer.webex.com/docs/security-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Build Responsibly
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/security-overview). [Full Markdown](../../../../docs/security-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Publish](003-before-you-publish.md)

## Article introduction

MCP servers allow AI agents and applications to connect with external tools, services, and data sources. Because these servers can expose tools that read data, send data, or take actions on behalf of a user or organization, it is important to connect only to MCP servers that you know and trust. Use this guide to understand what to review before connecting to an MCP server, and what to consider when building or publishing your own MCP server.

## Selected section

## Build Responsibly

If you are building an MCP server, design it with transparency and safety in mind. Clearly describe each tool, request only the permissions needed, avoid exposing unnecessary data, and make sure users understand what actions the server can perform.

Do not include malicious, misleading, or hidden behavior in tool definitions. A trusted MCP ecosystem depends on clear ownership, safe defaults, and responsible handling of user and organization data.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/security-overview
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommended Checklist
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/security-overview). [Full Markdown](../../../../docs/security-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Publish](003-before-you-publish.md)

## Article introduction

MCP servers allow AI agents and applications to connect with external tools, services, and data sources. Because these servers can expose tools that read data, send data, or take actions on behalf of a user or organization, it is important to connect only to MCP servers that you know and trust. Use this guide to understand what to review before connecting to an MCP server, and what to consider when building or publishing your own MCP server.

## Selected section

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

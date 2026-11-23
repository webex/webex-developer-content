---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-suite-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- What is Webex Suite MCP Server?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-suite-mcp-server). [Full Markdown](../../../../docs/webex-suite-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

## What is Webex Suite MCP Server?

Webex Suite MCP Server is a single MCP server that brings together core Webex capabilities across Meetings, Messaging, Calling, and Vidcast. Instead of connecting to a separate MCP server for each product area, users can connect once and use their AI client to perform common Webex workflows such as finding meetings, getting summaries and transcripts, searching messages, sending updates, sharing files, reviewing call insights, and accessing Vidcast transcripts or highlights.

It is designed to give knowledge workers a simple, secure, and unified way to use basic Webex Suite functionality from their preferred AI client.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

- **Server URL:** `https://mcp.webexapis.com/mcp/webex-suite`

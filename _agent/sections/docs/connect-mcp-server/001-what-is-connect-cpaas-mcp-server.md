---
type: Excerpt
canonical_url: https://developer.webex.com/docs/connect-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What is Connect CPaaS MCP Server?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/connect-mcp-server). [Full Markdown](../../../../docs/connect-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

## What is Connect CPaaS MCP Server?

Webex Connect CPaaS MCP Server connects AI tools and workflows to Webex Connect messaging capabilities. It enables agents and apps to discover sender IDs approved for a channel and business use case, and send governed, non-templated SMS and email using Webex Connect Send Message API v2.

This makes it easy to automate customer follow-ups, service-status updates, meeting summaries, reminders, supervisor alerts, and operational notifications while preserving tenant-level control over sender identities and permitted use cases.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details. Messaging through MCP must also be enabled in Webex Connect Tenant Settings, and at least one SMS phone number or supported email asset must be enabled for AI Agent Messaging and assigned one or more approved use cases.



> MCP server availability and your organization's endpoint require sign-in on the [official portal page](<https://developer.webex.com/docs/connect-mcp-server>).

The following authored configuration is availability-dependent:

**Server URL:** Use the MCP server URL that matches your Webex Connect tenant region.

| Connect Tenant Region | MCP Server URL |
| --- | --- |
| AWS Canada (ca) | [https://mcp.ca.webexconnect.io/mcp/cpaas](https://mcp.ca.webexconnect.io/mcp/cpaas) |
| AWS Ireland (eu) | [https://mcp.eu.webexconnect.io/mcp/cpaas](https://mcp.eu.webexconnect.io/mcp/cpaas) |
| AWS London (uk) | [https://mcp.uk.webexconnect.io/mcp/cpaas](https://mcp.uk.webexconnect.io/mcp/cpaas) |
| AWS Oregon (us) | [https://mcp.us.webexconnect.io/mcp/cpaas](https://mcp.us.webexconnect.io/mcp/cpaas) |
| AWS Mumbai (in) | [https://mcp.in.webexconnect.io/mcp/cpaas](https://mcp.in.webexconnect.io/mcp/cpaas) |
| AWS Sydney (au) | [https://mcp.au.webexconnect.io/mcp/cpaas](https://mcp.au.webexconnect.io/mcp/cpaas) |
| AWS Singapore (sg) | [https://mcp.sg.webexconnect.io/mcp/cpaas](https://mcp.sg.webexconnect.io/mcp/cpaas) |

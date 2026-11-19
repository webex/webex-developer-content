---
type: Guide
title: Webex MCP Server | Connect CPaaS MCP Server
display_title: Connect CPaaS MCP Server
canonical_url: https://developer.webex.com/docs/connect-mcp-server
content_type: documentation
product_group:
- webex-connect
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/connect-mcp-server)

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



## Tools

3 tools covering sender discovery and outbound SMS and email messaging:

| Tool | Description |
|------|-------------|
| `webex-sender-ids` | Returns sender IDs that the administrator has enabled for AI Agent Messaging. Results can be filtered by channel and use case so the agent selects an approved sender before sending. |
| `webex-sms-message` | Sends a non-templated SMS using an approved sender ID. The recipient must be in E.164 format, and the message body must not exceed 1,024 characters. Use `contentType` `text` for GSM 03.38 characters and `unicode` when the message contains characters outside GSM 03.38. |
| `webex-email-message` | Sends a non-templated plain-text or HTML email using an approved sender ID. Supports attachments. The body must not exceed 500,000 characters, and the total message size must not exceed 25 MB. |

## Connect to your MCP Client

Select your AI client to get connection instructions:

- [Amazon Quick](https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick)
- [Claude Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code)
- [Claude Desktop](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop)
- [Codex](https://developer.webex.com/docs/webex-agentic-mcp-servers-codex)
- [Copilot Studio](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio)
- [Cursor](https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor)
- [Gemini CLI](https://developer.webex.com/docs/webex-agentic-mcp-servers-gemini-cli)
- [VS Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode)

## Authentication

**Auth Type:** OAuth 2.0 Bearer Token

**Issuer:** `https://webexapis.com`

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server calls Webex Connect APIs on behalf of the authenticated user.

## Scopes

1 OAuth scope required:

| Scope | Description |
|-------|-------------|
| `spark:mcp` | Required for MCP server connection. |

**Full scope string:**

```sh
spark:mcp
```

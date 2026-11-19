---
type: Guide
title: Webex MCP Server | Meetings MCP Server
display_title: Meetings MCP Server
canonical_url: https://developer.webex.com/docs/meetings-mcp-server
content_type: documentation
product_group:
- webex-suite
categories:
- mcp
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/meetings-mcp-server)

## What is Meetings MCP Server?

Webex Meetings MCP Server connects AI tools and workflows to Webex Meetings capabilities. It enables agents and apps to schedule meetings, look up meeting details, and access meeting transcripts and transcript snippets for analysis or follow-up. This makes it easy to automate meeting coordination, generate summaries, extract action items, and build assistants that help teams get more value from their meetings. It is a strong fit for use cases like scheduling support, post-meeting recap generation, transcript search, and meeting intelligence workflows.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

- **Server URL:** `https://mcp.webexapis.com/mcp/webex-meeting`

## Tools

8 tools covering the full meeting lifecycle:

| Tool | Description |
|------|-------------|
| `webex-list-meetings` | List/search meetings with filters (date range, topic, state, type). Entry point for resolving meeting names to IDs. |
| `webex-create-meeting` | Create meetings with title, time, duration, invitees, recurrence, and password. Sends email invitations. |
| `webex-update-meeting` | Update meeting properties (title, time, agenda, recurrence) and manage invitees (add/update/remove). |
| `webex-delete-meeting` | Delete a scheduled meeting with optional cancellation email. |
| `webex-get-meeting-status` | Retrieve meeting details and optionally the live participant list. |
| `webex-get-meeting-summary` | Get AI-generated summary notes (HTML) and action items for ended meetings (requires Webex AI Assistant). |
| `webex-list-recordings` | List recording metadata with playback/download URLs and passwords. |
| `webex-list-transcripts` | List transcript metadata and optionally download full plain-text transcript content for LLM analysis. |

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

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server forwards it to each plugin, and plugins call the Webex REST API on behalf of the authenticated user.

## Scopes

7 unique OAuth scopes required:

| Scope | Used By |
|-------|---------|
| `spark:mcp` | Required for MCP server connection |
| `meeting:schedules_read` | `webex-list-meetings`, `webex-get-meeting-status`, `webex-list-transcripts` |
| `meeting:schedules_write` | `webex-create-meeting`, `webex-update-meeting`, `webex-delete-meeting` |
| `meeting:participants_read` | `webex-get-meeting-status` |
| `meeting:summaries_read` | `webex-get-meeting-summary` |
| `meeting:recordings_read` | `webex-list-recordings` |
| `meeting:transcripts_read` | `webex-list-transcripts` |

**Full scope string:**

```sh
spark:mcp meeting:schedules_read meeting:schedules_write meeting:participants_read meeting:summaries_read meeting:recordings_read meeting:transcripts_read
```

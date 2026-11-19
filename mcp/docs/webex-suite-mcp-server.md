---
type: Guide
title: Webex MCP Server | Webex Suite MCP Server
display_title: Webex Suite MCP Server
canonical_url: https://developer.webex.com/docs/webex-suite-mcp-server
content_type: documentation
product_group:
- webex-suite
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-suite-mcp-server)

## What is Webex Suite MCP Server?

Webex Suite MCP Server is a single MCP server that brings together core Webex capabilities across Meetings, Messaging, Calling, and Vidcast. Instead of connecting to a separate MCP server for each product area, users can connect once and use their AI client to perform common Webex workflows such as finding meetings, getting summaries and transcripts, searching messages, sending updates, sharing files, reviewing call insights, and accessing Vidcast transcripts or highlights.

It is designed to give knowledge workers a simple, secure, and unified way to use basic Webex Suite functionality from their preferred AI client.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

- **Server URL:** `https://mcp.webexapis.com/mcp/webex-suite`

## Tools

25 tools covering Meetings, Messaging, Vidcast, and Calling:

### Meetings (6)

| Tool | Description |
|------|-------------|
| `webex-list-meetings` | Lists the user's Webex meetings. |
| `webex-manage-meeting` | Creates, updates, or deletes a meeting (`webex-create-meeting`, `webex-update-meeting`, `webex-delete-meeting`). |
| `webex-get-meeting-status` | Retrieves the status of a meeting, including participant information. |
| `webex-get-meeting-summary` | Retrieves the AI-generated summary for a meeting. |
| `webex-list-recordings` | Lists recordings for the user's meetings. |
| `webex-list-transcripts` | Lists transcripts for the user's meetings. |

### Messaging (11)

| Tool | Description |
|------|-------------|
| `webex-manage-message` | Creates, edits, or deletes a message, or replies in a thread (`webex-create-message`, `webex-edit-message`, `webex-delete-message`, `webex-create-thread-reply`). |
| `webex-get-message` | Retrieves the details of a specific message. |
| `webex-search-messages` | Searches messages across the user's spaces. |
| `webex-manage-space` | Creates, updates, or deletes a space (`webex-create-space`, `webex-update-space`, `webex-delete-space`). |
| `webex-get-space` | Retrieves the details of a specific space. |
| `webex-search-spaces` | Searches the user's spaces. |
| `webex-manage-membership` | Adds, updates, or removes a space membership (`webex-add-membership`, `webex-update-membership`, `webex-remove-membership`). |
| `webex-upload-file` | Uploads a file to Webex. |
| `webex-share-file` | Shares a file to a space or message. |
| `webex-download-file` | Downloads file content from a message or space. |
| `webex-manage-webhook` | Creates, updates, or deletes a webhook (`webex-create-webhook`, `webex-update-webhook`, `webex-delete-webhook`). |

### Vidcast (5)

| Tool | Description |
|------|-------------|
| `vidcast-search-videos` | Searches Vidcast videos the user can access. |
| `vidcast-list-my-videos` | Lists the user's own Vidcast videos. |
| `vidcast-list-shared-with-me` | Lists Vidcast videos shared with the user. |
| `vidcast-get-video-transcript` | Retrieves the transcript for a Vidcast video. |
| `vidcast-get-video-highlights` | Retrieves the highlights for a Vidcast video. |

### Calling (3)

| Tool | Description |
|------|-------------|
| `webex-call-control` | Performs call control actions. |
| `webex-get-call-insights` | Retrieves insights for a call by call ID. |
| `webex-search-calls` | Searches calls by keyword(s) and date range. |

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

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server forwards it to the Webex APIs, which respond on behalf of the authenticated user.

## Scopes

| Scope | Used By |
|-------|---------|
| `spark:mcp` | Required for MCP server connection |
| `meeting:schedules_read` | `webex-list-meetings`, `webex-manage-meeting`, `webex-get-meeting-status`, `webex-list-transcripts` |
| `meeting:schedules_write` | `webex-manage-meeting` |
| `meeting:participants_read` | `webex-get-meeting-status` |
| `meeting:summaries_read` | `webex-get-meeting-summary` |
| `meeting:recordings_read` | `webex-list-recordings` |
| `meeting:transcripts_read` | `webex-list-transcripts` |
| `spark:messages_write` | `webex-manage-message`, `webex-upload-file`, `webex-share-file` |
| `spark:messages_read` | `webex-manage-message`, `webex-get-message`, `webex-download-file`, `webex-search-messages` |
| `spark:rooms_write` | `webex-manage-space` |
| `spark:rooms_read` | `webex-get-space`, `webex-search-spaces` |
| `spark:memberships_write` | `webex-manage-membership` |
| `spark:webhooks_write` | `webex-manage-webhook` |
| `Identity:Organization` | `vidcast-search-videos`, `vidcast-list-my-videos`, `vidcast-list-shared-with-me`, `vidcast-get-video-transcript`, `vidcast-get-video-highlights` |
| `Identity:Config` | `vidcast-search-videos`, `vidcast-list-my-videos`, `vidcast-list-shared-with-me`, `vidcast-get-video-transcript`, `vidcast-get-video-highlights` |

**Full scope string:**

```sh
spark:mcp meeting:schedules_read meeting:schedules_write meeting:participants_read meeting:summaries_read meeting:recordings_read meeting:transcripts_read spark:messages_write spark:messages_read spark:rooms_write spark:rooms_read spark:memberships_write spark:webhooks_write Identity:Organization Identity:Config
```

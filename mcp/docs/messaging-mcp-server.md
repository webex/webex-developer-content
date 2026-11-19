---
type: Guide
title: Webex MCP Server | Messaging MCP Server
display_title: Messaging MCP Server
canonical_url: https://developer.webex.com/docs/messaging-mcp-server
content_type: documentation
product_group:
- webex-suite
categories:
- mcp
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/messaging-mcp-server)

## What is Messaging MCP Server?

Webex Messaging MCP Server connects AI tools and workflows to Webex Messaging capabilities. It enables agents and apps to create, edit, delete, and retrieve messages in 1:1 and group spaces; manage spaces and memberships; and search messages, files, and spaces.

This makes it easy to automate team communications, route alerts and updates into the right spaces, streamline collaboration setup, support compliance and discovery workflows, and build assistants that help teams work more effectively inside Webex.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

- **Server URL:** `https://mcp.webexapis.com/mcp/webex-messaging`

## Tools

24 tools covering messaging, spaces, memberships, webhooks, files, and threading:

### Messages (5)

| Tool | Description |
|------|-------------|
| `webex-create-message` | Create a new message in a Webex space or 1:1 direct message. Supports plain text, markdown, HTML, file URL attachments, and adaptive card attachments. |
| `webex-edit-message` | Edit an existing message by messageId and roomId. Supports text or markdown only (not HTML). |
| `webex-delete-message` | Delete a message from a Webex space. Destructive and irreversible. Works for both 1:1 and group spaces. |
| `webex-get-message` | Retrieve a single message by ID or list messages in a room with optional filters (mentionedPeople, before/after, parentId). |
| `webex-search-messages` | Search messages in a Webex space by roomId with optional keyword query, date range, mentionedPeople, parentId, or hasFiles filters. |

### Spaces (5)

| Tool | Description |
|------|-------------|
| `webex-create-space` | Create a new Webex space (room) with title and optional teamId, isLocked, isAnnouncementOnly settings. |
| `webex-get-space` | Get a space by roomId or list spaces filtered by type (direct/group), teamId, and sortBy. |
| `webex-update-space` | Update space properties including title, isLocked, and isAnnouncementOnly. |
| `webex-delete-space` | Delete a space or remove the caller from it, depending on role. Deleted spaces cannot be recovered. |
| `webex-search-spaces` | Search spaces with type filter, teamId, and sortBy. |

### Memberships (4)

| Tool | Description |
|------|-------------|
| `webex-add-membership` | Add a member to a space by roomId and personId or personEmail. Optionally grant moderator privileges. |
| `webex-get-membership` | Get a membership by ID or list memberships filtered by roomId, personId, or personEmail. |
| `webex-update-membership` | Update membership properties such as moderator role or isRoomHidden. |
| `webex-remove-membership` | Remove a member from a space by membershipId. |

### Webhooks (4)

| Tool | Description |
|------|-------------|
| `webex-create-webhook` | Create a webhook for real-time event notifications (messages, memberships, rooms, meetings, recordings, etc.) with optional filter and HMAC secret. |
| `webex-get-webhook` | Get a webhook by ID or list all webhooks. |
| `webex-update-webhook` | Update webhook name, targetUrl, secret, and status. |
| `webex-delete-webhook` | Delete a webhook by webhookId. |

### Files (4)

| Tool | Description |
|------|-------------|
| `webex-share-file` | Share files in a Webex space by attaching public file URLs to messages. |
| `webex-upload-file` | Upload a file to a Webex space via base64-encoded content with fileName and contentType. |
| `webex-get-file-details` | Get file metadata (Content-Type, Content-Length, Content-Disposition) from a Webex message file URL. |
| `webex-download-file` | Download file content from a Webex message file URL. Returns base64-encoded content. |

### Threading (2)

| Tool | Description |
|------|-------------|
| `webex-create-thread-reply` | Create a threaded reply to a message in a Webex space. Requires roomId, parentId, and text or markdown. |
| `webex-get-thread` | Get all threaded replies for a parent message by roomId and parentId. |

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

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server forwards it to each plugin, and plugins call the Webex REST API (webexapis.com) on behalf of the authenticated user.

## Scopes

9 unique OAuth scopes required:

| Scope | Used By |
|-------|---------|
| `spark:mcp` | Required for MCP server connection |
| `spark:messages_read` | `webex-get-message`, `webex-search-messages`, `webex-get-file-details`, `webex-download-file`, `webex-get-thread` |
| `spark:messages_write` | `webex-create-message`, `webex-edit-message`, `webex-delete-message`, `webex-share-file`, `webex-upload-file`, `webex-create-thread-reply` |
| `spark:rooms_read` | `webex-get-space`, `webex-search-spaces` |
| `spark:rooms_write` | `webex-create-space`, `webex-update-space`, `webex-delete-space` |
| `spark:memberships_read` | `webex-get-membership` |
| `spark:memberships_write` | `webex-add-membership`, `webex-update-membership`, `webex-remove-membership` |
| `spark:webhooks_read` | `webex-get-webhook` |
| `spark:webhooks_write` | `webex-create-webhook`, `webex-update-webhook`, `webex-delete-webhook` |

**Full scope string:**

```sh
spark:mcp spark:messages_read spark:messages_write spark:rooms_read spark:rooms_write spark:memberships_read spark:memberships_write spark:webhooks_read spark:webhooks_write
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/messaging-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/messaging-mcp-server). [Full Markdown](../../../../docs/messaging-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

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

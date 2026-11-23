---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-suite-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-suite-mcp-server). [Full Markdown](../../../../docs/webex-suite-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

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

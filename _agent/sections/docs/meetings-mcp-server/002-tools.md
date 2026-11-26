---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings-mcp-server
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings-mcp-server). [Full Markdown](../../../../docs/meetings-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

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

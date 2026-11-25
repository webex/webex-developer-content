---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings-mcp-server). [Full Markdown](../../../../docs/meetings-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md)

## Selected section

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

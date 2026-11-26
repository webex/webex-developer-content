---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-suite-mcp-server
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-suite-mcp-server). [Full Markdown](../../../../docs/webex-suite-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md)

## Selected section

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

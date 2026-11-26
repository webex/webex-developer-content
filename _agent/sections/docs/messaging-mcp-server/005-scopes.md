---
type: Excerpt
canonical_url: https://developer.webex.com/docs/messaging-mcp-server
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/messaging-mcp-server). [Full Markdown](../../../../docs/messaging-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md)

## Selected section

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

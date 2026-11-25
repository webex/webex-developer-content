---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server). [Full Markdown](../../../../docs/contact-center-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](005-authentication.md)

## Selected section

## Scopes

5 OAuth scopes required:

| Scope | Used By |
|-------|---------|
| `spark:mcp` | Required to connect through the Webex MCP server platform. |
| `cjp:config_read` | `wxcc-list-flows`, `wxcc-get-flow`, `wxcc-validate-flow`, `wxcc-get-flow-template`, `wxcc-get-activity-definitions`, `wxcc-describe-activity`, `wxcc-list-event-specifications`, `wxcc-get-choices`, `wxcc-view-config`, `wxcc-realtime` (list event types; list/get subscriptions), `wxcc-journey-get-customer-context`. |
| `cjp:config_write` | `wxcc-create-flow`, `wxcc-save-flow-draft`, `wxcc-patch-flow-draft`, `wxcc-admin-config`, `wxcc-realtime` (create/update/delete subscriptions), `wxcc-journey-get-customer-context`. |
| `cjp:user` | `wxcc-realtime` (WebSocket session provisioning: subscribe-realtime-data, subscribe-notification), `wxcc-journey-get-customer-context`. |
| `spark:people_read` | `wxcc-copilot-run-search-query` (resolves caller's orgId via Webex People API). |

**Full scope string:**

```sh
spark:mcp cjp:config_read cjp:config_write cjp:user spark:people_read
```

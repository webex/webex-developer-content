---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspaces-mcp-server
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspaces-mcp-server). [Full Markdown](../../../../docs/workspaces-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md)

## Selected section

## Scopes

5 unique OAuth scopes required:

| Scope | Used By |
|-------|---------|
| `spark:mcp` | Required for MCP server connection |
| `spark-admin:devices_read` | `device_aggregated_event_history`, `device_configuration_diff`, `device_configuration_list`, `device_configuration_schema`, `device_configuration_template_diff`, `device_configuration_template_list`, `device_error_code_detail_search`, `device_event_history`, `device_search`, `product_lifecycle` |
| `spark-admin:workspace_metrics_read` | `workspace_aggregated_capacity_utilization`, `workspace_aggregated_popularity_metrics`, `workspace_aggregated_usage_metrics`, `workspace_metrics` |
| `spark-admin:workspaces_read` | `workspace_search` |
| `spark-admin:workspace_locations_read` | `location_search` |

**Full scope string:**

```sh
spark:mcp spark-admin:devices_read spark-admin:workspace_metrics_read spark-admin:workspaces_read spark-admin:workspace_locations_read
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspaces-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspaces-mcp-server). [Full Markdown](../../../../docs/workspaces-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md) [Scopes](005-scopes.md)

## Selected section

## Tools

16 tools covering device intelligence, configuration management, workspace utilization, and location data:

### Devices (10)

| Tool | Description |
|------|-------------|
| `device_aggregated_event_history` | Gets organization-wide device history events with filters, pagination, and event aggregations. |
| `device_configuration_diff` | Compares configuration values between two devices. |
| `device_configuration_list` | Lists the actual current configuration keys and values for a specific device. |
| `device_configuration_schema` | Searches possible configuration keys and allowed values across device models in the organization. |
| `device_configuration_template_diff` | Compares a device's actual configuration against a named configuration template. |
| `device_configuration_template_list` | Lists configuration templates available in the organization. |
| `device_error_code_detail_search` | Searches device and workspace issue definitions, error codes, descriptions, and recommended actions. |
| `device_event_history` | Gets recent history events for a specific device by device ID. |
| `device_search` | Searches devices using filters, sorting, pagination, aggregations, and output formats. |
| `product_lifecycle` | Gets lifecycle milestones for Cisco device product types, such as end-of-sale or last support dates. |

### Workspaces (5)

| Tool | Description |
|------|-------------|
| `workspace_aggregated_capacity_utilization` | Finds overcrowded or under-utilized workspaces across the organization. |
| `workspace_aggregated_popularity_metrics` | Ranks the most popular workspaces by actual use time or booking time. |
| `workspace_aggregated_usage_metrics` | Gets aggregate workspace usage or booking metrics over time. |
| `workspace_metrics` | Retrieves historical utilization or environmental metrics for specific workspaces. |
| `workspace_search` | Searches workspaces with filters, sorting, aggregations, paging, and output format options. |

### Locations (1)

| Tool | Description |
|------|-------------|
| `location_search` | Searches organization locations by name, city, address, location ID, or floor count. |

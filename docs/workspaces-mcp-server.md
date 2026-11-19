---
type: Guide
title: Webex MCP Server | Workspaces MCP Server
display_title: Workspaces MCP Server
canonical_url: https://developer.webex.com/docs/workspaces-mcp-server
content_type: documentation
product_group:
- webex-suite
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/workspaces-mcp-server)

## What is Workspaces MCP Server?

Transform IT operations with real-time workspace and device intelligence, bringing Webex Control Hub's workspace and device data into your agentic platforms. Monitor health, resolve hardware issues fast, and unlock utilization insights to spot issues early and optimize meeting spaces.

> **Prerequisites:** This MCP server must be enabled by your organization's admin in Webex Control Hub before it can be used. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

- **Server URL:** `https://mcp.webexapis.com/mcp/workspaces`

Before you can set up this MCP server, the Workspaces Agentic App and its tools have to be enabled in Control Hub. See [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) for details.

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

**Auth Type:** OAuth 2.0 using client ID & secret, or Webex Agentic App token

**Issuer:** `https://webexapis.com`

**Flow:** The MCP client obtains a Webex OAuth token and passes it via the `Authorization: Bearer <token>` header. The server forwards it to each plugin, and plugins call the Webex REST API on behalf of the authenticated user.

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

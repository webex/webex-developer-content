---
type: Guide
title: Webex MCP Server | Contact Center MCP Server
display_title: Contact Center MCP Server
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/contact-center-mcp-server)

## What is Contact Center MCP Server?

The Webex Contact Center MCP Server enables AI agents and automation tools to securely interact with Webex Contact Center capabilities on behalf of authenticated users.

It supports Day 0 administration and Flow Designer operations, including creating, updating, and deleting entry points, business hours, dial plans, and dial numbers; reviewing read-only configuration for queues and teams; searching and managing flows; creating and updating drafts; modifying nodes and edges; and validating flow definitions.

The server also provides AI-generated customer context by alias, including concise summaries, insights, and frequently discussed topics, without exposing transcripts, prompts, or internal evidence. Real-time capabilities enable agents to manage webhook subscriptions for telemetry events and provision WebSocket sessions for use cases such as live wallboards and supervisor dashboards.

Administrators enable and govern the server through the Webex Agentic Platform or the Agentic Apps settings in Control Hub.

The current flow authoring contract is FlowV2, and activity discovery uses ActivityV2, a condensed schema designed for API and LLM clients.

> **Prerequisites:** Administrators must enable the Webex Contact Center MCP Server for the organization through Webex Agentic Platform / Control Hub Agentic Apps settings before users can connect supported MCP clients. Administrators can also control which Contact Center MCP tools are enabled for the organization, including the Flow Designer tools listed below.



> MCP server availability and your organization's endpoint require sign-in on the [official portal page](<https://developer.webex.com/docs/contact-center-mcp-server>).



## Tools

16 tools cover flow management, activity discovery, validation, choices, events, templates, customer journey, real-time subscriptions, admin configuration, and historical analytics.

### Flow Management (6)

| Tool | Description |
|------|-------------|
| `wxcc-list-flows` | List or search flows and subflows. Supports all flows, a single flow by ID, name filtering, full-text search, flow type, and pagination. |
| `wxcc-create-flow` | Create a new flow from a FlowV2 object. Supports overwrite mode for an existing flow with the same name. |
| `wxcc-get-flow` | Read a flow by ID. Defaults to the draft; use the version parameter for latest or a specific version ID. |
| `wxcc-save-flow-draft` | Replace the current draft of an existing flow with a full FlowV2 object. Supports optimistic locking through expected_version. |
| `wxcc-patch-flow-draft` | Partially update an existing draft by upserting or removing nodes and edges, or by shallow-merging top-level fields. The server validates the result before saving. |
| `wxcc-validate-flow` | Validate a persisted draft/version by flow ID, or dry-run validate a FlowV2 object without saving. |

### Templates, Activities, and Choices (5)

| Tool | Description |
|------|-------------|
| `wxcc-get-flow-template` | Return a starter FlowV2 template for a flow or subflow. Templates can include a minimal skeleton or IVR menu starter nodes. |
| `wxcc-get-activity-definitions` | List core and logic activity definitions from the activity registry as ActivityV2. Supports flow type, UI-enabled filtering, search, and exact activity-name lookup. |
| `wxcc-describe-activity` | Describe one activity as ActivityV2, including inputs, outputs, output ports, and authoring notes. |
| `wxcc-list-event-specifications` | List known event specification triplets for start and event nodes, such as contact-start and global-error handling events. |
| `wxcc-get-choices` | Resolve static, searchable, validated, or cascading choices for one activity input, such as queues, entry points, teams, skills, flows, or media files. |

### Admin Tools (2)

| Tool | Description |
|------|-------------|
| `wxcc-view-config` | Read Webex Contact Center configuration resources (entry-point, business-hours, dial-plan, dial-number, skill-profile, auxiliary-code, team, user, agent-profile, outdial-ani, contact-service-queue). Supports list and get operations. Read-only. |
| `wxcc-admin-config` | Create, update, or delete Webex Contact Center configuration resources (entry-point, business-hours, dial-plan, dial-number). Destructive write tool. Uses optimistic concurrency via version field. Requires a user account context. |

### Real-Time & Subscriptions (1)

| Tool | Description |
|------|-------------|
| `wxcc-realtime` | Manage Webex Contact Center real-time telemetry subscriptions and bootstrap live sessions. Actions: discover event types; list, get, create, update, and delete webhook subscriptions (V2) for pushed events; and provision WebSocket sessions (subscribe-realtime-data, subscribe-notification) that return a webSocketUrl and subscriptionId for a client to connect and consume live queue/agent telemetry. Used for wallboards and supervisor dashboards. Destructive; requires a user account context. |

### Customer Journey (1)

| Tool | Description |
|------|-------------|
| `wxcc-journey-get-customer-context` | Retrieve AI-generated customer context by alias, including concise summaries, insights, and frequently discussed topics—without exposing transcripts, prompts, or internal evidence. Read-only. |

### Historical Analytics (1)

| Tool | Description |
|------|-------------|
| `wxcc-copilot-run-search-query` | Run a read-only GraphQL query against the Webex Contact Center Search API. Returns rows or aggregations for historical analytics (CSR, ASR, CLR record types). Use as an advanced escape hatch for custom Contact Center reporting when standard tools cannot cover the request. Shared with the Contact Center Operation MCP Server. Read-only and non-destructive. |

## Authoring Model

Use FlowV2 for flow create, read, save, patch, export, and validation workflows.

| Concept | How to use it |
|---------|---------------|
| FlowV2 | The flow authoring object. Top-level fields include schemaVersion, id, orgId, projectId, flowType, name, version, variables, nodes, edges, and eventFlows. |
| Nodes | Each node uses a unique name, a coarse activityType, and activity-specific properties. The specific activity is identified by properties.activityName. |
| Edges | Edges connect node names with from, to, and condition. Edge conditions should come from ActivityV2.outputPorts[].condition. |
| ActivityV2 | The activity discovery schema. Use `wxcc-get-activity-definitions` or `wxcc-describe-activity` before authoring activity nodes. |
| Choices | Use `wxcc-get-choices` for org-specific input values instead of guessing IDs or display names. |

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

**Auth Type:** OAuth 2.0 Bearer Token

**Issuer:** `https://webexapis.com`

**Flow:** The MCP client obtains a Webex OAuth token and passes it in the `Authorization: Bearer <token>` header. The server validates organization access and forwards the token to FlowV2 REST API calls on behalf of the authenticated user.

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

## Access and Guardrails

- Users must have access to the target Webex Contact Center organization.
- Read tools require configuration read permission. Write tools require configuration write permission and a user account context.
- The server validates `orgId` for every tool call because organization ID is supplied as a tool argument.
- The server applies guardrails for per-organization/per-tool rate limits, write payload size, maximum nodes, maximum edges, and downstream service failures.
- Write tools validate and normalize FlowV2 before saving. A flow should be validated before any publish or production lifecycle action outside this MCP tool surface.

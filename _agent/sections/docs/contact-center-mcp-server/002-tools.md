---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Tools
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server). [Full Markdown](../../../../docs/contact-center-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](005-authentication.md) [Scopes](006-scopes.md)

## Selected section

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

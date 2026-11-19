---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Flow document structure
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Flow document structure

A Flow document has a small set of top-level fields plus arrays of nodes, edges, and variables, a single event-flow object, and an array of preferences.

### Top-level fields

| Property | Type | Notes |
| --- | --- | --- |
| `name` | string | Name of the flow. Must be unique in the project unless you import with `overwrite=true`. |
| `flowType` | enum | `FLOW` or `SUBFLOW`. |
| `contactType` | string | Channel type — for example `telephony`, `customMessaging`, `workItem`, `genericAction`. |
| `description` | string | Human-readable description. |
| `version` | integer | Monotonically increasing document version. Server-assigned; do not set it on import. |
| `status` | enum | `Draft` or `Published`. Server-managed. |
| `nodes` | array | Activity nodes in the main flow process. Must include exactly one `start` node. |
| `edges` | array | Edges connecting nodes in the main flow process. |
| `variables` | array | Flow variables. |
| `eventFlows` | object | A single event-handler process (`nodes` and `edges`) that runs when a bound event fires. |
| `preferences` | array | Flow-level preferences. |

### Node

A node represents one activity instance. Nodes appear in `nodes[]` and in the event flow's `nodes[]`.

| Field | Notes |
| --- | --- |
| `id` | Stable, unique node identifier within the flow. |
| `name` | Node name. Referenced by edges (`from`/`to`) and used as the merge key for `PATCH` (`upsert_nodes`, `remove_node_names`). |
| `activityType` | Category of node: `start`, `action`, `event`, or `end`. A flow must contain exactly one `start` node. |
| `properties` | Activity configuration. Always includes `properties.activityName` (the activity this node runs, matching an `activityName` from `listActivityDefinitions`); the remaining keys are the activity's input values and depend on the activity definition. |

### Edge

| Field | Notes |
| --- | --- |
| `id` | Stable, unique edge identifier within the flow. Also the merge key for `PATCH` (`upsert_edges`, `remove_edge_keys`). |
| `from` | Source node `name`. |
| `to` | Target node `name`. |
| `condition` | Branch condition the edge fires on. Aliases `done` → `out` and `defaultBranch` → `default` are normalized server-side. |
| `properties` | Optional edge properties — for example, the condition value for a branching port. |

### Variable

| Field | Notes |
| --- | --- |
| `name` | Variable name. |
| `type` | Data type, e.g. `STRING`, `INTEGER`, `BOOLEAN`. |
| `value` | Default value, encoded as a string. |
| `description` | Human-readable description. |
| `isCAD` | `true` if exposed as Call-Associated Data. |
| `isAgentEditable` | `true` if agents can edit the value at runtime. |
| `isReportable` | `true` if included in reporting. |
| `isSecure` | `true` if the value is sensitive and must be masked in logs and reports. |

### Event flow

The `eventFlows` field is a single object with its own `nodes` and `edges`:

| Field | Notes |
| --- | --- |
| `nodes` | Activity nodes in the event-handler process. |
| `edges` | Edges in the event-handler process. |

An event handler begins with an **event node** (`activityType: "event"`) whose `properties.eventSpecificationName` names the event it reacts to (along with `eventSourceName` and `eventClassificationName`). A **global error handler** is simply an event flow whose event node binds the global-error event. You build its `nodes` and `edges` exactly like the main flow.

### Preference

A preference is a flow-level setting:

| Field | Notes |
| --- | --- |
| `name` | Preference name, e.g. `hideSecureCADWarning`. |
| `type` | Preference value type, e.g. `Boolean`. |
| `value` | Value, encoded as a string. |

### Ports and conditions

A minimal flow is three nodes wired in a line:

```text
NewContact  --(condition: out)-->  WelcomeMessage  --(condition: default)-->  DisconnectContact
```

An activity exposes named **output ports** (discoverable via `describeActivity` as `outputPorts[]`, where each port is `{ condition, label, isErrorPath }` — for example `{ "condition": "default" }` or `{ "condition": "error", "isErrorPath": true }`). Ports are discovery metadata — they are not named directly on the edge. Instead, an edge selects which branch it represents through its `condition`, and for a branching port the specific value goes in the edge's `properties`.

When you import or validate a flow, the server enforces three rules. Keep them in mind while assembling the document by hand:

1. Every edge's `from` and `to` must reference a node `name` that exists in the **same** process (the main flow, or the event flow).
2. An edge's `condition` must correspond to a real output of the source node's activity — it matches one of the activity's `outputPorts[].condition`, after the aliases `done` → `out` and `defaultBranch` → `default` are normalized.
3. Node `name` values and edge `id` values must be unique within a process, and the main process must contain exactly one `start` node.

---
type: Guide
title: Getting Started with Flow Orchestration | Consolidated Guide
display_title: Getting Started with Flow Orchestration
canonical_url: https://developer.webex.com/docs/flow-orchestration
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/flow-orchestration)

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Introduction

A flow is a directed graph that describes the logical steps of a contact-center interaction. Each box on the canvas is a **node** that runs one **activity** — play a prompt, queue a contact, end the interaction — and the arrows between boxes are **edges** that decide which node runs next.

The Flow Orchestration APIs let you discover the activities and events available in your project, assemble those nodes and edges into a Flow JSON document, validate it, and import it as a draft on the tenant — the same headless `discover → assemble → validate → import` loop that AI-assisted flow authoring builds on.

A Flow document is made up of these pieces:

- **Start node** — the single entry point. It has `activityType: "start"` and `properties.activityName: "start"`. Its `properties.flowType` carries the trigger binding (`eventSourceName`, `eventClassificationName`, `eventSpecificationName`); for inbound telephony the `eventSpecificationName` is `ContactStartWorkflow`.
- **Action nodes** — the work the flow does. They have `activityType: "action"` and name the activity in `properties.activityName` (for example `play-message`).
- **End node** — terminates the interaction. It has `activityType: "end"`, for example `properties.activityName: "disconnect-contact"`.
- **Edges** — connect nodes and select which branch fires through the edge's `condition` (and, for a branching port, the edge's `properties`).
- **Variables** — named values the flow reads and writes.
- **Event flow** — a separate node/edge graph that runs when a bound event fires (this is how a global error handler is modeled).
- **Preferences** — flow-level settings.

Activity names, event names, and input fields are discovered per project at runtime — this guide uses the canonical values returned for a telephony project, but you should read the values for your own project from the discovery endpoints in [Before you begin](https://developer.webex.com/docs/flow-orchestration#before-you-begin).

## Before you begin

You need:

- A Webex Contact Center administrator access token. See [Authentication](https://developer.webex.com/docs/authentication) for how to obtain one.
- Scopes: `cjp:config_read` for the discovery calls, and `cjp:config_write` for validate and import.
- The base URL for your organization's region (see the table below). Webex Contact Center is served from region-specific gateways; use the one your tenant is provisioned in.
- Your organization ID (`{orgId}`) and the project ID (`{projectId}`). The `{orgId}` must be the organization **UUID** (for example `8eb7da9a-c81c-4d13-b08b-38fdeb7330d8`); the Spark-encoded organization ID returned by some generic Webex APIs is not accepted by this gateway. The project ID is a system-generated value that is the same across orgs and environments — always use `5e5c9ad6d61f870d6d778c1b`.

| Region | Base URL |
| --- | --- |
| Integration | `https://api.intgus1.ciscoccservice.com` |

All requests send the token in the `Authorization` header:

```text
Authorization: Bearer <YOUR_ACCESS_TOKEN>
```

The examples below use the shell variables `${TOKEN}` and `${ORG_ID}` for these values, and `${BASE_URL}` for your region's gateway from the table above — for example `export BASE_URL="https://api.intgus1.ciscoccservice.com"`.

### Discover activities

A flow can only reference activities that exist in your project. List them — along with their `group`, input fields, output ports, and the JSON Schema for their inputs — with `listActivityDefinitions`. The response is self-describing and sufficient on its own to construct nodes:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/activities" \
  -H "Authorization: Bearer ${TOKEN}"
```

Each activity reports an `activityName` and a `group` that classifies it. Read both from the discovery response rather than assuming a fixed set or naming convention — `activityName` values are project-specific and their casing varies (for example `start`, `play-message`, `SetCallerID`, `Feedback-V2`), and `group` is an open set (for example `action`, `terminating-action`, `enum-gateway`). Pick the activities you need by matching on the discovered values:

- **Start** — the activity whose `activityName` is `start`.
- **Play a prompt** — `play-message`.
- **End the flow** — a terminating activity, for example `disconnect-contact`.

To inspect one activity's full input/output/port schema, call `describeActivity` with its `activityName`:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/activities/play-message" \
  -H "Authorization: Bearer ${TOKEN}"
```

When an input takes a value from a constrained set (a priority, an audio file, a team), resolve the allowed values with `getActivityInputChoices`. Call it with no parameters to list all choices; pass `search=<text>` to filter (type-ahead); add `validate=true` to do a point-lookup of a single value (matched against the choice's `value`/ID, not its display name). For a **cascading** input whose values depend on a sibling input, supply the parent with `parentInputName=<name>` and `parentValue=<value>` — otherwise the call returns `400`. The endpoint is only valid for inputs that expose choices — an input the `describeActivity` definition marks with `allowedValues` or a `choicesEndpoint`; calling it for any other input name returns `400`. Filtering and validation apply to dynamic (`choicesEndpoint`-backed) inputs; a static input (for example `voiceLanguage`) always returns its full enumerated list. Use the exact input name from `describeActivity`:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/activities/queue-contact/inputs/destination/choices?parentInputName=channelType&parentValue=TELEPHONY" \
  -H "Authorization: Bearer ${TOKEN}"
```

### Discover events

An event flow can only react to events your project exposes. List them with `listEventSpecifications`:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/event-specifications" \
  -H "Authorization: Bearer ${TOKEN}"
```

Each result's `name` is what you put into an event node's `properties.eventSpecificationName`. Find the global-error event in this list and use its `name` for the event node in [Add a global error handler](https://developer.webex.com/docs/flow-orchestration#add-a-global-error-handler).

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

## Build a basic flow

This first flow greets the caller with a prompt and then ends:

```text
NewContact  -->  WelcomeMessage  -->  DisconnectContact
```

### Step 1 — Assemble the flow document

Save the following as `flow.json`. The activity names (`start`, `play-message`, `disconnect-contact`) are the canonical values for a telephony project; confirm yours with [Discover activities](https://developer.webex.com/docs/flow-orchestration#before-you-begin).

```json
{
  "name": "SamplePlayMessageFlow",
  "flowType": "FLOW",
  "contactType": "telephony",
  "description": "Minimal sample flow: greet the caller, then disconnect.",
  "variables": [],
  "nodes": [
    {
      "id": "node-start",
      "name": "NewContact",
      "activityType": "start",
      "properties": {
        "activityName": "start",
        "flowType": {
          "eventSourceName": "WebexContactCenter",
          "eventClassificationName": "VoiceInteractions",
          "eventSpecificationName": "ContactStartWorkflow"
        }
      }
    },
    {
      "id": "node-welcome",
      "name": "WelcomeMessage",
      "activityType": "action",
      "properties": {
        "activityName": "play-message",
        "prompt": {
          "promptType": "text",
          "text": "Thank you for calling. Goodbye.",
          "textType": "text"
        }
      }
    },
    {
      "id": "node-end",
      "name": "DisconnectContact",
      "activityType": "end",
      "properties": {
        "activityName": "disconnect-contact"
      }
    }
  ],
  "edges": [
    {
      "id": "edge-1",
      "from": "NewContact",
      "to": "WelcomeMessage",
      "condition": "out",
      "properties": {}
    },
    {
      "id": "edge-2",
      "from": "WelcomeMessage",
      "to": "DisconnectContact",
      "condition": "default",
      "properties": {}
    }
  ],
  "preferences": [
    { "name": "hideSecureCADWarning", "type": "Boolean", "value": "true" }
  ]
}
```

The node `name` values (`NewContact`, `WelcomeMessage`, `DisconnectContact`) are human-readable labels and can be anything unique within the process — it is the `activityType` and `properties.activityName` that determine what each node does. Note how the three rules from [Ports and conditions](https://developer.webex.com/docs/flow-orchestration#flow-document-structure) hold: the two edges reference existing node names, each fires on a condition the source activity exposes, and the node names and edge IDs are all unique.

The `play-message` node's `properties.prompt` shown here is the shape the API returns in its examples; the exact inputs an activity accepts are defined by its `describeActivity` schema, so confirm the input names for your project.

### Step 2 — Validate (dry run)

Validate the document before persisting it. This does not create anything:

```bash
curl -sS -X POST \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/flows:validate" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data @flow.json
```

A valid document returns `valid: true` with an empty `errors` array. The response also carries a `warnings` array (non-blocking recommendations) and a human-readable `summary`:

```json
{
  "valid": true,
  "errors": [],
  "warnings": [],
  "summary": "FlowV2 looks valid for import/save."
}
```

If something is wrong, validation tells you why:

```json
{
  "valid": false,
  "errors": [
    {
      "activityName": "play-message",
      "condition": "onTimeout",
      "from": "WelcomeMessage",
      "edge": "WelcomeMessage->DisconnectContact(onTimeout)",
      "suggestion": "Use one of: default, error",
      "message": "Condition 'onTimeout' is not valid for activity 'play-message'.",
      "severity": "ERROR"
    }
  ],
  "warnings": [],
  "summary": "1 error(s), 0 warning(s)."
}
```

Validation and import do not enforce exactly the same rules, and the difference runs both ways: `:validate` can reject a document that `:import` would accept (for example, an edge whose `condition` is not a real output port fails `:validate` with `valid: false`, yet still imports with `201`), and some checks are only meaningful at import time. Treat a successful validation as necessary, not sufficient — and always handle a possible error on `:import`.

### Step 3 — Import the draft

Import the document. This creates the flow in `Draft` state and returns its metadata, including the assigned `flow.id`:

```bash
curl -sS -X POST \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/flows:import?overwrite=false&flowType=FLOW" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data @flow.json
```

A successful import returns `201 Created`. The flow document is returned under `flow`, alongside any non-blocking `preflightWarnings` raised while persisting it:

```json
{
  "flow": {
    "id": "661c7bc712eaf357de7e4aeb",
    "orgId": "8eb7da9a-c81c-4d13-b08b-38fdeb7330d8",
    "version": 0,
    "flowType": "FLOW",
    "name": "SamplePlayMessageFlow",
    "description": "Minimal sample flow: greet the caller, then disconnect.",
    "status": "Draft",
    "createdBy": "user@example.com",
    "createdDate": "2026-01-15T09:12:00.000Z",
    "lastModifiedBy": "user@example.com",
    "lastModifiedDate": "2026-01-15T09:12:00.000Z"
  },
  "preflightWarnings": [],
  "preflightWarningsCount": 0
}
```

Two error responses are worth knowing:

- `409 Conflict` — a flow with the same `name` already exists and `overwrite` is `false`. Re-import with `overwrite=true` or choose a new name.
- `400 Bad Request` — the document failed a structural check (for example a missing or duplicate start node, an edge referencing a node that does not exist, or an unreadable JSON body). An unknown `activityName` surfaces as `500` with a `type` of `ACTIVITY_NOT_FOUND`. Import errors do **not** use the validate call's `{ "valid": false, "errors": [...] }` shape — the body is `{ "status", "errors": [...], "trackingId" }`, where each `errors` entry is either a plain message string or a `{ "description", "type" }` object; there is no JSON-pointer `path` field.

The server assigns the flow's `flow.id` and authoritative `flow.version`; do not rely on the `version` you send in the body (you manage version explicitly only when saving a draft — see [Modify a draft incrementally](https://developer.webex.com/docs/flow-orchestration#modify-a-draft-incrementally)).

### Step 4 — Verify

Fetch the persisted draft by its `flow.id` to confirm it was stored as expected:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/flows/661c7bc712eaf357de7e4aeb" \
  -H "Authorization: Bearer ${TOKEN}"
```

You can also re-validate the stored draft with `GET …/v2/flows/{flowId}:validate?versionId=draft` (note this is a `GET` — unlike the stateless document `:validate`, which is a `POST` — and it returns its findings under a `results` array rather than `errors`), or export it for backup with `GET …/v2/flows/{flowId}:export?version=latest`.

### Validation errors

When `valid` is `false` (or you receive a `422`), each entry in `errors[]` identifies the offending element. The fields present depend on the failure; the entries you get most often carry:

| Field | Notes |
| --- | --- |
| `message` | Human-readable explanation — surface this to the author. |
| `suggestion` | Corrective hint when available, e.g. `Use one of: default, error`. |
| `severity` | `ERROR` or a warning severity. |
| `activityName` | The activity involved, when the error is activity-specific. |
| `condition` / `from` / `edge` | For edge/port errors: the offending `condition`, the source node `from`, and a readable `edge` label. |

Common causes:

| Cause | What it means |
| --- | --- |
| Unknown activity | A node's `properties.activityName` is not in `listActivityDefinitions`. |
| Invalid port | An edge's `condition` is not an output port the source activity exposes. |
| Unknown input value | An input value is not in the resolved choice set for that input. |

The error object leads with `message` (and often `suggestion`); it does not always include a stable machine-readable `code`, so surface `message` to the author rather than keying logic off a code. Always read `message` for the specifics.

## Add a global error handler

This second flow keeps the same main process and adds an event flow that runs when the global-error event fires. The handler ends the contact:

```text
main:    NewContact  -->  WelcomeMessage  -->  DisconnectContact
handler: GlobalErrorHandling  -->  EndOnError      (runs on the global-error event)
```

### Step 1 — Add the event flow

The main `nodes` and `edges` are unchanged. `eventFlows` is a single object with its own `nodes` and `edges`. The handler's first node is an **event node** whose `properties.eventSpecificationName` is the event `name` you found in [Discover events](https://developer.webex.com/docs/flow-orchestration#before-you-begin) — here, `GlobalErrorHandling`.

```json
{
  "name": "SamplePlayMessageFlowWithErrorHandler",
  "flowType": "FLOW",
  "contactType": "telephony",
  "description": "Sample flow with a global error handler event flow.",
  "variables": [],
  "nodes": [
    {
      "id": "node-start",
      "name": "NewContact",
      "activityType": "start",
      "properties": {
        "activityName": "start",
        "flowType": {
          "eventSourceName": "WebexContactCenter",
          "eventClassificationName": "VoiceInteractions",
          "eventSpecificationName": "ContactStartWorkflow"
        }
      }
    },
    {
      "id": "node-welcome",
      "name": "WelcomeMessage",
      "activityType": "action",
      "properties": {
        "activityName": "play-message",
        "prompt": {
          "promptType": "text",
          "text": "Thank you for calling. Goodbye.",
          "textType": "text"
        }
      }
    },
    {
      "id": "node-end",
      "name": "DisconnectContact",
      "activityType": "end",
      "properties": {
        "activityName": "disconnect-contact"
      }
    }
  ],
  "edges": [
    {
      "id": "edge-1",
      "from": "NewContact",
      "to": "WelcomeMessage",
      "condition": "out",
      "properties": {}
    },
    {
      "id": "edge-2",
      "from": "WelcomeMessage",
      "to": "DisconnectContact",
      "condition": "default",
      "properties": {}
    }
  ],
  "eventFlows": {
    "nodes": [
      {
        "id": "event-global-error",
        "name": "GlobalErrorHandling",
        "activityType": "event",
        "properties": {
          "activityName": "event",
          "eventSourceName": "WebexContactCenter",
          "eventClassificationName": "VoiceInteractions",
          "eventSpecificationName": "GlobalErrorHandling"
        }
      },
      {
        "id": "event-end",
        "name": "EndOnError",
        "activityType": "end",
        "properties": {
          "activityName": "disconnect-contact"
        }
      }
    ],
    "edges": [
      {
        "id": "event-edge-1",
        "from": "GlobalErrorHandling",
        "to": "EndOnError",
        "condition": "out",
        "properties": {}
      }
    ]
  },
  "preferences": [
    { "name": "hideSecureCADWarning", "type": "Boolean", "value": "true" }
  ]
}
```

Two things to note:

- The main process and the event flow are independent scopes. Node names, edge IDs, and conditions only have to be unique *within* their own process, which is why the handler can reuse the `disconnect-contact` activity under a new node name (`EndOnError`).
- The event node is the handler's entry point: it binds the event via `properties.eventSpecificationName`, and an edge leads from it into the handling activities. There is no top-level `event` field — the binding lives entirely on the event node.

### Step 2 — Validate and import

Validate and import exactly as in [Build a basic flow](https://developer.webex.com/docs/flow-orchestration#build-a-basic-flow) — the same `…:validate` and `…:import` calls apply. Import validates the entire document, including the event flow, so a problem inside `eventFlows` (for example an unknown event on an event node, or an unknown `activityName` in the handler) is reported in the same import error envelope described above — a message in `errors[]`, not a JSON-pointer `path`.

## Modify a draft incrementally

Once a draft exists you rarely rewrite the whole document. There are two ways to change it.

### Save a flow draft

Replace the whole draft with the Save Flow Draft operation — `POST …/v2/flows/{flowId}?expectedVersion=N`. Pass `expectedVersion` to enable optimistic locking; the request fails with `409 Conflict` if the flow's version has moved on. Omit it to skip the check. The response is the same metadata envelope as import (`flow`, `preflightWarnings`, `preflightWarningsCount`). Note that a draft save does not increment `flow.version` on its own — `expectedVersion` guards against a published version that has moved on, so repeated saves within the same version are not distinguished by the version number.

### Patch a flow draft

Apply a partial change with the Patch Flow Draft operation — `PATCH …/v2/flows/{flowId}`. The body is a patch contract; the merge happens server-side, is idempotent, and is re-validated, so the draft is never left broken:

```json
{
  "upsert_nodes": [
    {
      "id": "node-hold",
      "name": "HoldMessage",
      "activityType": "action",
      "properties": {
        "activityName": "play-message",
        "prompt": {
          "promptType": "text",
          "text": "Thanks for calling. Please hold.",
          "textType": "text"
        }
      }
    }
  ],
  "upsert_edges": [
    {
      "id": "edge-3",
      "from": "WelcomeMessage",
      "to": "HoldMessage",
      "condition": "out",
      "properties": {}
    }
  ],
  "remove_node_names": [],
  "remove_edge_keys": []
}
```

`upsert_nodes` matches existing nodes by `name` and `upsert_edges` matches by `id` — present items are replaced, new ones are added. `remove_node_names` deletes nodes by `name` and `remove_edge_keys` deletes edges by `id`; if you remove a node, remove the edges that reference it in the same patch or the merged document fails validation. A `PATCH` body may also carry top-level overrides such as `name` and `description`.

This is what makes a hand-authored flow *expandable*: start from the atomic flow above, then grow it one patch at a time.

## Build a custom function

A **custom function** is a small piece of user-authored code (JavaScript or Python) that a flow can call to transform data — parse a JSON payload, normalize a phone number, look up a value. Functions are managed by the Custom Functions API. Unlike the flow endpoints, its paths are not scoped to a project:

- The base URL is the same regional gateway (`${BASE_URL}`) used for the flow endpoints — see the region table in [Before you begin](https://developer.webex.com/docs/flow-orchestration#before-you-begin).
- Function paths are `/v1/{orgId}/functions…` — there is no `{projectId}` segment.
- Scopes: `cjp:config_read` to list, get, and export; `cjp:config_write` to create, update, test, publish, lock, unlock, and import. The `Authorization: Bearer ${TOKEN}` header is the same as before.

This walkthrough builds a `parseContact` function that takes a contact record and returns the caller's phone digits and area code, then tests and publishes it. Once published, a function can be referenced from a flow.

A function exports a single `handle` entry point. It reads its declared inputs from `request.inputs`, writes its result to `response.data`, and returns the `response`:

```js
export const handle = async (request, response) => {
  const phoneDigits = String(request.inputs.contact.phone).replace(/\D/g, "");
  response.data = {
    phoneDigits,
    areaCode: phoneDigits.slice(0, 3)
  };
  return response;
};
```

### Step 1 — Create the function

`sourceCode` is sent as an escaped string. `inputs[]` declares each input's `name`, `dataType` (one of `boolean`, `datetime`, `decimal`, `integer`, `json`, `string`), and a sample `value`. `outputs` is a stringified JSON object mapping each output name to a sample value. `language` is `js` or `py`. `selectedRuntime` is case-sensitive and defaults to the highest supported runtime for the language (for example `nodejs22.x` for `js`, or `python3.13` for `py`). `timeoutInSec` caps execution time.

```bash
curl -sS -X POST \
  "${BASE_URL}/v1/${ORG_ID}/functions" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data '{
    "name": "parseContact",
    "description": "Parses a contact record: strips the phone to digits and extracts the area code.",
    "language": "js",
    "selectedRuntime": "nodejs22.x",
    "timeoutInSec": 3,
    "sourceCode": "export const handle = async (request, response) => {\n  const phoneDigits = String(request.inputs.contact.phone).replace(/\\D/g, \"\");\n  response.data = { phoneDigits, areaCode: phoneDigits.slice(0, 3) };\n  return response;\n};",
    "inputs": [
      {
        "name": "contact",
        "dataType": "json",
        "value": "{\"name\":\"John Doe\",\"phone\":\"(415) 555-0132\"}"
      }
    ],
    "outputs": "{\"phoneDigits\":\"4155550132\",\"areaCode\":\"415\"}"
  }'
```

A successful create returns `201 Created`. The source code is returned under `fnCode` and the server-side metadata — including the assigned `id` and a `Draft` status — under `fnMetadata`:

```json
{
  "fnCode": "export const handle = async (request, response) => {\n  const phoneDigits = String(request.inputs.contact.phone).replace(/\\D/g, \"\");\n  response.data = { phoneDigits, areaCode: phoneDigits.slice(0, 3) };\n  return response;\n};",
  "fnMetadata": {
    "id": "64f1b2c3d4e5f6a7b8c9d0e1",
    "orgId": "8eb7da9a-c81c-4d13-b08b-38fdeb7330d8",
    "name": "parseContact",
    "description": "Parses a contact record: strips the phone to digits and extracts the area code.",
    "language": "js",
    "selectedRuntime": "nodejs22.x",
    "status": "Draft",
    "timeoutInSec": 3,
    "tagVersionMap": {},
    "lockedBy": "",
    "createdBy": "user@example.com",
    "createdDate": "2026-01-15T09:12:00.000Z",
    "lastModifiedBy": "user@example.com",
    "lastModifiedDate": "2026-01-15T09:12:00.000Z"
  }
}
```

### Step 2 — Test it

Run the function with a test payload. `inputs` is a JSON object whose keys match the declared input names — here, the John Doe contact:

```bash
curl -sS -X POST \
  "${BASE_URL}/v1/${ORG_ID}/functions/64f1b2c3d4e5f6a7b8c9d0e1:test" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data '{
    "inputs": {
      "contact": {
        "name": "John Doe",
        "phone": "(415) 555-0132"
      }
    }
  }'
```

The response carries the function's `response.data` in `data`, along with the HTTP `statusCode`, an `errorMessage` (empty on success), and the execution time in `timeTakenInMilliseconds`:

```json
{
  "statusCode": 200,
  "data": {
    "phoneDigits": "4155550132",
    "areaCode": "415"
  },
  "errorMessage": "",
  "timeTakenInMilliseconds": 12
}
```

The test call implicitly publishes the latest draft before running, so it always executes your most recent source code.

### Step 3 — Publish it

Publish the draft under one or more tags (`Dev`, `Test`, `Latest`, `Live`) to make a version addressable:

```bash
curl -sS -X POST \
  "${BASE_URL}/v1/${ORG_ID}/functions/64f1b2c3d4e5f6a7b8c9d0e1:publish" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data '{ "tags": ["Live"], "comment": "Initial release." }'
```

Publishing returns the same `{ "fnCode", "fnMetadata" }` envelope, with the new tag reflected in `fnMetadata.tagVersionMap`. The published function can now be referenced from a flow.

### Function lifecycle reference

The rest of the lifecycle follows the same pattern:

- `GET …/v1/{orgId}/functions` and `GET …/v1/{orgId}/functions/{id}` — list and inspect.
- `PUT …/v1/{orgId}/functions/{id}` — update the draft (same body shape as create).
- `…/v1/{orgId}/functions/{id}:export` returns the function definition as a JSON object (`name`, `language`, `runtime`, `description`, `sourceCode`, `inputs`, `outputs`), and `…/v1/{orgId}/functions:import` accepts that JSON object as a multipart file upload — together they move a function between environments.
- `…/v1/{orgId}/functions/{id}:lock` and `:unlock` coordinate concurrent edits; each returns the JSON string `"OK"`.

## Restrictions

1. A flow's main process must contain exactly one start node (`activityType: "start"`). A document without one is rejected by both `:validate` (`valid: false`) and `:import` (`400`).
2. A flow `name` must be unique within the project unless you import with `overwrite=true`; otherwise import returns `409 Conflict`.
3. `:validate` and `:import` do not enforce identical rules — passing `:validate` does not guarantee `:import` will succeed, and `:validate` may reject a document (for example an invalid edge `condition`) that `:import` still accepts.
4. Node `name` values and edge `id` values must be unique within their process, and an edge may only reference nodes in the same process (no edges between the main flow and the event flow).
5. When patching a draft, edges that reference a removed node must be removed in the same patch, or the merged document fails validation.
6. A custom function `name` must be unique within the organization; a duplicate name returns `409 Conflict`.
7. Save and patch requests that pass `expectedVersion` fail with `409 Conflict` if the server-side draft version has moved on.
8. The Flow Orchestration API does not expose a delete operation for flows — an imported flow persists as tenant state. In shared or test tenants, prefix flow names (for example `WXCC_TEST_`) so they are easy to identify, and remove them through Control Hub when you are done.

## Recommendations and best practices

- Discover before you author. List activities with `listActivityDefinitions` and events with `listEventSpecifications`, and use the returned `activityName` values and event `name`s verbatim rather than hard-coding them or assuming a naming convention — the discovery responses are self-describing.
- Validate before importing, but treat a successful `:validate` as necessary, not sufficient; always handle a possible `422` on `:import`.
- Resolve constrained inputs (queues, audio files, teams) with `getActivityInputChoices` instead of guessing values, to avoid `UNKNOWN_*` validation errors.
- Use `PATCH` for incremental edits, and pass `expectedVersion` to enable optimistic locking when multiple editors or automations touch the same draft.
- Surface the validation `message` (and `suggestion` when present) to the author; the error shape does not always include a stable machine-readable `code`, so don't rely on one for control flow.
- For custom functions, test (`:test`) before publishing, and publish under explicit tags (`Dev`/`Test`/`Latest`/`Live`) so versions stay addressable.
- Keep sensitive values in `isSecure` variables so they are masked in logs and reports.

## Next steps

- **Publish.** This guide stops at the validated draft. Publishing a draft (and the lock/unlock that goes with editing) is a separate step in the Flows API — see the Flow Orchestration API reference.
- **Expand the flow.** Discover more activities with `listActivityDefinitions`, resolve their inputs with `getActivityInputChoices`, and add them with `PATCH`. Routing activities (for example, queueing a contact) follow the same node/edge pattern shown here.
- **Automate authoring.** Because a flow is just a Flow JSON document validated by the `…:validate` endpoint, the discover → assemble → validate → import loop in this guide is the same foundation that AI-assisted flow authoring builds on.

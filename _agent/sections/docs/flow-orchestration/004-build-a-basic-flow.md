---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build a basic flow
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

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

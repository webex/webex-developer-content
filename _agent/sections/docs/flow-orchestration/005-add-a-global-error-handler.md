---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Add a global error handler
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

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

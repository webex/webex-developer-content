---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- getTaskMap()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-call-control). [Full Markdown](../../../../docs/desktop-call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Retrieve tasks and control interactions, WebRTC calls, and call recording from Desktop widgets.

## Parent context

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

## Selected section

### getTaskMap()

Retrieves the full list of tasks that are assigned to an agent at a given time.

**Example**

```javascript
const currentTaskMap = await Desktop.actions.getTaskMap();
// => Get current task map from Desktop store
```

Returns
`{Map}` A list of results.

**Example Response**

```text
Desktop Store TaskMap:
    Map(1) {
        "851a8e81-6150-11eb-9a47-f1ca3756d4bd" => {
            …}, "eed4b53a-614f-11eb-9a47-8be6439707ee" => {
            …}
    }
    [
        [Entries]
    ] {
        "851a8e81-6150-11eb-9a47-f1ca3756d4bd" => Object
    }
key: "851a8e81-6150-11eb-9a47-f1ca3756d4bd"
value:
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701"
eventType: "RoutingMessage"
interaction: {
    callAssociatedData: {
        …},
    callAssociatedDetails: {
        …},
    callFlowParams: {
        …},
    callProcessingDetails: {
        …},
    contactDirection: {
        …},
    …
}
interactionId: "851a8e81-6150-11eb-9a47-f1ca3756d4bd"
mediaResourceId: "4D44FF32-A585-4DD8-8422-4920FC97066A@cisco.com"
orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25"
queueMgr: "aqm"
trackingId: "69773a10-6163-11eb-9fb9-8dadf7aee433"
type: "AgentContactAssigned"
```

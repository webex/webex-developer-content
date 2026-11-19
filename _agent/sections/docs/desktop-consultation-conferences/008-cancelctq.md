---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- cancelCtq()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-consultation-conferences). [Full Markdown](../../../../docs/desktop-consultation-conferences.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Use the Desktop SDK to consult agents and queues and manage conference participants.

## Parent context

## Agent Contact Methods

These methods belong to `Desktop.agentContact`. Use the V2 method where the older method is marked for deprecation.

## Selected section

### cancelCtq()

Cancels a consult to queue request.

**Example**

```javascript
await Desktop.agentContact.cancelCtq({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    data: {
        agentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
        queueId: "3268"
    }
});

```

**Payload type**

```typescript
type CancelCtqPayload = {
    interactionId: string;
    data: { agentId: string; queueId: string };
};
```

The following table lists the payload details:

| Name          | Type   | Description                                 | Required |
| ------------- | ------ | ------------------------------------------- | -------- |
| interactionId | String | Unique identifier for the user interaction. | Yes      |
| data          | Object | Options of the consult to queue request.    | Yes      |
| -->agentId    | String | Unique identifier of the agent.             | Yes      |
| -->queueId    | String | Unique identifier of the queue.             | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `AgentCtqCancelled`; else, `AgentCtqCancelFailed`.

**Example Response**

```javascript
const cancelCtqResponse = {
  data: {
    agentId: "a96ffe92-f5c8-4715-9427-fa32a7e57ccc",
    eventType: "RoutingMessage",
    interaction: {
      callAssociatedData: {},
      callAssociatedDetails: {},
      callFlowParams: {},
      callProcessingDetails: {},
      contactDirection: {
        type: "INBOUND"
      },
      currentVTeam: "",
      interactionId: "9ad96648-415b-11eb-881c-ed6dd0d45a04",
      isFcManaged: false,
      isTerminated: false,
      media: {},
      mediaChannel: "none",
      mediaType: "none",
      orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
      outboundType: null,
      owner: null,
      participants: {},
      previousVTeams: [],
      state: "none"
    },
    interactionId: "c8e35eec-a977-409b-922d-7d2825c63cf2",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueId: "7352",
    queueMgr: "aqm",
    trackingId: "ee2bc7e0-50c8-11eb-a1f8-5d0ad357b8a5",
    type: "AgentCtqCancelled"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_908141bb-3f1f-43fe-b7e2-5a132c97745f",
  type: "RoutingMessage"
};
```

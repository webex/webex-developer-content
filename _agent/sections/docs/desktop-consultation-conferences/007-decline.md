---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- decline()
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

### decline()

Declines a consult request.

**Example**

```javascript
await Desktop.agentContact.decline({
    interactionId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3",
    data: {
        mediaResourceId: "c837e6f7-699a-4736-bb82-03a6d58bb7f3"
    },
    isConsult: true,
});
```

**Payload type**

```typescript
type RequestPayload = {
    interactionId: string;
    data: declinePayload;
    isConsult: boolean
}

type declinePayload = {
    mediaResourceId: string;
};
```

The following table lists the payload details:

| Name          | Type    | Description                                                                                                                                   | Required |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String  | Unique identifier for the user interaction.                                                                                                   | Yes      |
| data | Object | Options of the decline request. | Yes |
| -->mediaResourceId | String | Identifier of the media resource being declined. | Yes |
| isConsult     | Boolean | Determines whether the task request is consult or not.<br><br>- True—The task request is consult.<br>- False—The task request is not consult. | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, and `isConsult` is _true_, the value is `AgentConsultFailed`; else, `AgentOfferContactRona`.

**Example Response**

```javascript
const declineResponse = {
  data: {
    agentId: "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
    destAgentId: "f795f41f-3782-44fa-97a4-c8b4dc029477",
    destinationType: "Agent",
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
      state: "none",
      workflowManager: null
    },
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b",
    orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
    queueMgr: "aqm",
    reason: "Test",
    reasonCode: 500,
    trackingId: "2037cb70-653d-11eb-8a11-a3c35f103d4b",
    type: "AgentConsultFailed"
  },
  orgId: "f111e3af-1a45-42ef-9erf-4562354b8a25",
  trackingId: "notifs_a241b1c4-3d42-4ad0-8738-71b1e7611550",
  type: "RoutingMessage"
};
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- dropConferenceParticipant()
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

### dropConferenceParticipant()

Removes a participant from an active conference.

**Note:** Only the primary agent on the conference can drop other participants from the conference.

**Example**

```javascript
await Desktop.agentContact.dropConferenceParticipant({
    interactionId: "706fa9d9-7561-4f57-b306-62bfaa5285db",
    data: {
        participantId: "66809250-2cb9-411a-8c63-8cab91bc4d1b"
    }
});

```

The following table lists the payload details:

| Name             | Type   | Description                                                          | Required |
| ---------------- | ------ | ---------------------------------------------------------------------- | -------- |
| interactionId    | String | Unique identifier for the user interaction.                            | Yes      |
| data             | Object | Options of the drop conference participant request.                   | Yes      |
| -->participantId | String | Unique identifier of the participant to remove from the conference.   | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The `type` parameter value in the response payload depends on the success or failure of the method. If the method is successful, the value is `ParticipantLeftConference`; else, `ParticipantDropConferenceFailed`.

**Example Response**

```javascript
const dropConferenceParticipantResponse = {
  "data": {
    "droppedById": "b99c0871-b4da-4f36-9346-5bc1021e9a52",
    "eventTime": 1783673778329,
    "eventType": "RoutingMessage",
    "interaction": {
      "callAssociatedData": {
        // Nested fields omitted for brevity.
      },
      "callAssociatedDetails": {
        // Nested fields omitted for brevity.
      },
      "callFlowParams": {},
      "callProcessingDetails": {
        // Nested fields omitted for brevity.
      },
      "campaignOutboundType": null,
      "contactDirection": { "type": "INBOUND" },
      "createdTimestamp": 1783673737101,
      "currentVTeam": "a943338b-2920-48c1-a05e-bbe0a326c02a",
      "flowProperties": null,
      "interactionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
      "isFcManaged": true,
      "isMediaForked": false,
      "isTerminated": false,
      "mainInteractionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
      "media": {
        // Nested fields omitted for brevity.
      },
      "mediaChannel": "telnyx",
      "mediaProperties": null,
      "mediaType": "telephony",
      "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
      "outboundType": null,
      "owner": "b99c0871-b4da-4f36-9346-5bc1021e9a52",
      "parentInteractionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
      "participants": {
        // Nested fields omitted for brevity.
      },
      "previousVTeams": ["6941634b-c781-4d0a-8d70-bd2a2174dcd7"],
      "queuedTimestamp": null,
      "segments": {
        // Nested fields omitted for brevity.
      },
      "state": "connected",
      "workflowManager": null
    },
    "interactionId": "706fa9d9-7561-4f57-b306-62bfaa5285db",
    "leftParticipant": null,
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "participantId": "66809250-2cb9-411a-8c63-8cab91bc4d1b",
    "participantType": "Agent",
    "queueMgr": "aqm",
    "reason": null,
    "reasonCode": null,
    "trackingId": "d8593cf5-8a6e-4ab4-a09e-64df1ab08497",
    "type": "ParticipantLeftConference"
  },
  "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
  "trackingId": "notifs_705a6646-2185-4752-a5d6-1a7c1dd579ab",
  "type": "RoutingMessage"
};
```

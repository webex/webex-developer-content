---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-consultation-conferences
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Methods
- exitConference()
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

### exitConference()

exits a conference request.
**Note:** The end consult call feature is enabled using the `isEndConsultEnabled` payload. For more information, see [Agent State Information Module](https://developer.webex.com/docs/desktop-agent-state#agent-state-information-module).

**Example**

```javascript
await Desktop.agentContact.exitConference({
    interactionId: "a26d035d-b547-11ea-984b-d3128111ce6b"
});

```

**Payload type**

```typescript
type ExitConferencePayload = {
    interactionId: string;
};
```

The following table lists the payload details:

| Name          | Type    | Description                                                                                                                                   | Required |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| interactionId | String  | Unique identifier for the user interaction.                                                                                                   | Yes      |

**Returns**
`{Object}` The object with the retrieved data.

**Note:** The successful response example has `type: "AgentConsultConferenceEnded"`. Subscribe to `eAgentConsultConferenceEndFailed` to handle a failed conference-end request; see [Contact Events and Subscriptions](https://developer.webex.com/docs/desktop-contact-events#eagentconsultconferenceendfailed).

**Example Response**

```javascript
const exitConferenceResponse = {
  "data": {
    "agentId": "366f2a3a-dd91-482f-b57e-1abf93dda1f7",
    "consultMediaResourceId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
    "destAgentId": "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7",
    "destinationType": "Agent",
    "eventTime": 1728979843658,
    "eventType": "RoutingMessage",
    "force": false,
    "interaction": {
      "callAssociatedData": {
        "CallDate": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "CallDate",
          "global": false,
          "isSecure": false,
          "name": "CallDate",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "DATETIME",
          "value": "2024-10-15T08:09:54.214Z[UTC]"
        },
        "Customer_Name": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Customer_Name",
          "global": false,
          "isSecure": false,
          "name": "Customer_Name",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "ModiJi"
        },
        "Global_FeedbackSurveyOptIn": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Post Call Survey Opt-in",
          "global": true,
          "isSecure": false,
          "name": "Global_FeedbackSurveyOptIn",
          "reportable": true,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "uninitialized"
        },
        "Global_Language": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "Customer Language",
          "global": true,
          "isSecure": false,
          "name": "Global_Language",
          "reportable": true,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "en-US"
        },
        "Global_TestKey": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Global Test Key",
          "global": true,
          "isSecure": true,
          "name": "Global_TestKey",
          "reportable": false,
          "secureKeyId": "root",
          "secureKeyVersion": 3,
          "type": "STRING",
          "value": "eYXFa2Myvp7U0sIDvJDtKw==."
        },
        "TestKey": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "Test Key 1",
          "global": false,
          "isSecure": false,
          "name": "TestKey",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "TestValue"
        },
        "TestSameerGlobal": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "TestGlobal",
          "global": true,
          "isSecure": false,
          "name": "TestSameerGlobal",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "Sameer-value"
        },
        "ani": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "ani",
          "global": false,
          "isSecure": false,
          "name": "ani",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "9487554325"
        },
        "dn": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "dn",
          "global": false,
          "isSecure": false,
          "name": "dn",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "+15109024298"
        },
        "ronaTimeout": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "ronaTimeout",
          "global": false,
          "isSecure": false,
          "name": "ronaTimeout",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "25"
        },
        "test3": {
          "agentEditable": true,
          "agentViewable": true,
          "displayName": "test3-new",
          "global": false,
          "isSecure": false,
          "name": "test3",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "INTEGER",
          "value": "0"
        },
        "virtualTeamName": {
          "agentEditable": false,
          "agentViewable": true,
          "displayName": "virtualTeamName",
          "global": false,
          "isSecure": false,
          "name": "virtualTeamName",
          "reportable": false,
          "secureKeyId": "",
          "secureKeyVersion": 0,
          "type": "STRING",
          "value": "Queue_MCM"
        }
      },
      "callAssociatedDetails": {
        "ani": "9487554325",
        "dn": "+15109024298",
        "ronaTimeout": "25",
        "virtualTeamName": "Queue_MCM"
      },
      "callFlowParams": {},
      "callProcessingDetails": {
        "CONSULTED_AGENT_QUEUE_ID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "CONTINUE_RECORDING_ON_TRANSFER": "true",
        "EP_ID": "8befa99f-903e-4c33-8311-19666546b810",
        "QMgrName": "aqm",
        "QueueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "ani": "9487554325",
        "checkAgentAvailability": "false",
        "customerRegion": "intgus1",
        "dnis": "+15109024298",
        "fcDesktopView": "eNqVj0EKwjAQRe8y6xSsuuoFXAhump2ITHUWgXQSxzQgJXe3Ikg0irob/n8D/43gna9cJIFmOwJjT9AAsgEFEcVgZ6ml05TNIKkHcOSir/M+GgkDWk3Yb27JKzzPYXGM2vTkhlCAixzUdA5ruhTQEtJOgeFAgodgHFcemexfRt8W178uflJbWdeh3X8aXti100ly/3qrma7bbY9I",
        "fceRegisteredEvents": "",
        "flowTagId": "Latest",
        "isParked": "false",
        "mohFileName": "defaultmusic_on_hold.wav",
        "participantInviteTimeout": "false",
        "pauseDuration": "15",
        "pauseResumeEnabled": "true",
        "priority": "10",
        "queuedDestinationID": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "queuedTo": "Queue",
        "recordInProgress": "true",
        "recordingStarted": "true",
        "ronaTimeout": "25",
        "taskToBeSelfServiced": "false",
        "tenantId": "58f1a59e-245c-4536-9ee4-06560658e493",
        "virtualTeamName": "Queue_MCM",
        "vteamId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
        "workflowId": "62a165a995fe092e845f4804",
        "workflowName": "FlowSameer"
      },
      "contactDirection": { "type": "INBOUND" },
      "createdTimestamp": 1728979793852,
      "currentVTeam": "0025a125-4d2c-4e1a-833d-909e95a389cc",
      "interactionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
      "isFcManaged": true,
      "isMediaForked": false,
      "isTerminated": false,
      "mainInteractionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
      "media": {
        "0b09cfec-feea-4ccf-a78a-b7b06d485be2": {
          "holdTimestamp": null,
          "isHold": false,
          "mType": "mainCall",
          "mediaMgr": "callmm",
          "mediaResourceId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
          "mediaType": "telephony",
          "participants": ["9487554325", "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7"]
        }
      },
      "mediaChannel": "telnyx",
      "mediaProperties": null,
      "mediaType": "telephony",
      "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
      "outboundType": null,
      "owner": "366f2a3a-dd91-482f-b57e-1abf93dda1f7",
      "parentInteractionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
      "participants": {
        "366f2a3a-dd91-482f-b57e-1abf93dda1f7": {
          "autoAnswerEnabled": true,
          "bnrDetails": null,
          "callerId": null,
          "channelId": "7be4ef42-e2d8-450c-b89c-84c966539fc0",
          "consultState": null,
          "consultTimestamp": null,
          "deviceCallId": null,
          "deviceId": null,
          "deviceType": null,
          "dn": "webrtc-366f2a3a-dd91-482f-b57e-1abf93dda1f7",
          "hasJoined": true,
          "hasLeft": true,
          "id": "366f2a3a-dd91-482f-b57e-1abf93dda1f7",
          "isConsulted": false,
          "isInPredial": false,
          "isOffered": true,
          "isWrapUp": true,
          "isWrappedUp": false,
          "joinTimestamp": 1728979798880,
          "lastUpdated": 1728979843589,
          "name": "vik intg3",
          "pType": "Agent",
          "queueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
          "queueMgrId": "aqm",
          "sessionId": "226f136d-c3ac-4440-98c8-e4ff2ada91b2",
          "siteId": "b302fbf4-28b8-4b56-add0-162e2464db89",
          "skillId": null,
          "skillName": null,
          "skills": [],
          "teamId": "bdd276cd-d051-4b80-bd6e-9fb9eec18b99",
          "teamName": "Team-Minions",
          "type": "Agent",
          "wrapUpTimestamp": 1728979843589
        },
        "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7": {
          "autoAnswerEnabled": false,
          "bnrDetails": null,
          "callerId": null,
          "channelId": "83160396-10a1-460b-bc12-9d151050fb08",
          "consultState": null,
          "consultTimestamp": null,
          "deviceCallId": null,
          "deviceId": null,
          "deviceType": null,
          "dn": "webrtc-3b05f0e9-48e5-40c9-8923-c50e9b0b22a7",
          "hasJoined": true,
          "hasLeft": false,
          "id": "3b05f0e9-48e5-40c9-8923-c50e9b0b22a7",
          "isConsulted": false,
          "isInPredial": false,
          "isOffered": true,
          "isWrapUp": false,
          "isWrappedUp": false,
          "joinTimestamp": 1728979815616,
          "lastUpdated": 1728979815616,
          "name": "vik intg2",
          "pType": "Agent",
          "queueId": "0025a125-4d2c-4e1a-833d-909e95a389cc",
          "queueMgrId": "aqm",
          "sessionId": "b97fc378-c09d-43f0-8bf0-18294ab8d208",
          "siteId": "b302fbf4-28b8-4b56-add0-162e2464db89",
          "skillId": null,
          "skillName": null,
          "skills": [],
          "teamId": "bdd276cd-d051-4b80-bd6e-9fb9eec18b99",
          "teamName": "Team-Minions",
          "type": "Agent",
          "wrapUpTimestamp": null
        },
        "9487554325": {
          "callerId": null,
          "hasJoined": true,
          "hasLeft": false,
          "id": "9487554325",
          "isInPredial": false,
          "pType": "Customer",
          "type": "Customer"
        }
      },
      "previousVTeams": ["8befa99f-903e-4c33-8311-19666546b810"],
      "queuedTimestamp": null,
      "state": "connected",
      "workflowManager": null
    },
    "interactionId": "0b09cfec-feea-4ccf-a78a-b7b06d485be2",
    "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
    "queueMgr": "aqm",
    "trackingId": "05bcf437-d798-4c85-a70e-ce711de3c785",
    "type": "AgentConsultConferenceEnded"
  },
  "orgId": "58f1a59e-245c-4536-9ee4-06560658e493",
  "trackingId": "notifs_2a563687-b74d-4cbb-8679-94aa349c5a13",
  "type": "RoutingMessage"
}
```

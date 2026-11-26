---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Interaction
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## Interaction
The `interaction` field in the payload contains a comprehensive object with details about the interaction.

> ⚠️ **Disclaimer** :
> In Websocket event payloads, the interaction object contains internal state and data used for call-control and routing decisions.
> Some fields are not part of the public API contract.
> We recommend that you do not rely on fields in the interaction object until the new contract is published.


```json
{
  "interactionId": "66a872f1-8502-44ef-a71d-d8867374bfa0",
  "orgId": "22a3b45d-34b4-4f1d-b6c1-8d94524d0ff4",
  "state": "connected",
  "owner": "28a87164-4c54-420f-bb4c-c617748b82e6",
  "mediaType": "telephony",
  "mediaChannel": "provider-name",
  "media": {
    "0acae8f9-9000-4c04-9472-05291e081ed2": {
      "mediaResourceId": "0acae8f9-9000-4c04-9472-05291e081ed2",
      "mType": "mainCall",
      "mediaMgr": "media-manager",
      "mediaType": "telephony",
      "participants": [
        "customer-id",
        "28a87164-4c54-420f-bb4c-c617748b82e6"
      ],
      "isHold": false,
      "holdTimestamp": null
    }
  },
  "participants": {
    "customer-id": {
      "id": "customer-id",
      "pType": "Customer",
      "hasJoined": true,
      "isInPredial": false,
      "callerId": null,
      "hasLeft": false,
      "type": "Customer"
    },
    "28a87164-4c54-420f-bb4c-c617748b82e6": {
      "id": "28a87164-4c54-420f-bb4c-c617748b82e6",
      "sessionId": "86c4143a-8c60-4105-953b-f81f353b1604",
      "pType": "Agent",
      "queueMgrId": "queue-manager",
      "name": "Agent Name",
      "dn": "+10000000000",
      "queueId": "d2eddc63-5b32-4bb9-b7eb-8606e15b0992",
      "siteId": "site-id-1234",
      "teamId": "team-123",
      "teamName": "TeamName",
      "hasJoined": true,
      "isWrapUp": false,
      "isConsulted": false,
      "lastUpdated": 1700000000000,
      "channelId": "7662cfb0-a8be-42ba-b074-a37f86a57f44",
      "joinTimestamp": 1700000000000,
      "wrapUpTimestamp": null,
      "consultState": null,
      "consultTimestamp": null,
      "skills": [
        {
          "skillId": "c9108a20-8fa0-4c46-aaf3-bf8318e8faf3",
          "skillName": "SkillName",
          "skillType": "proficiency",
          "skillValue": "8",
          "agentId": "28a87164-4c54-420f-bb4c-c617748b82e6",
          "isDynamicSkill": false
        }
      ],
      "skillId": "primary-skill-id",
      "skillName": "PrimarySkill",
      "isOffered": true,
      "autoAnswerEnabled": false,
      "isInPredial": false,
      "callerId": null,
      "bnrDetails": null,
      "isWrappedUp": false,
      "hasLeft": false,
      "deviceType": null,
      "deviceCallId": null,
      "deviceId": null,
      "currentState": null,
      "currentStateTimestamp": null,
      "type": "Agent"
    }
  },
  "callProcessingDetails": {
    "QMgrName": "queue-manager",
    "routingStrategyId": "routing-strategy-uuid",
    "skillList": "[{\"skillType\":\"proficiency\",\"skillId\":\"skill-uuid\",\"skillName\":\"SkillName\",\"operand\":\"gte\",\"skillValue\":\"1\"}]",
    "participantInviteTimeout": "false",
    "ROUTING_TYPE": "queueBasedRouting",
    "isParked": "false",
    "flowTagId": "FlowTag",
    "checkAgentAvailability": "true",
    "tenantId": "tenant-001",
    "fceRegisteredEvents": "",
    "vteamId": "d2eddc63-5b32-4bb9-b7eb-8606e15b0992",
    "removeSkillsOnTransferToQueue": "false",
    "requiredSkillList": "[{\"skillType\":\"proficiency\",\"skillId\":\"skill-uuid\",\"skillName\":\"SkillName\",\"operand\":\"gte\",\"skillValue\":\"1\"}]",
    "skillRelaxations": "[]",
    "workflowName": "WorkflowName",
    "virtualTeamName": "VirtualTeamName",
    "priority": "10",
    "EP_ID": "044838e8-8295-4c21-9f4e-a07ee5712201",
    "taskToBeSelfServiced": "false",
    "contactAssignmentType": "ACD",
    "ani": "anonymous-number",
    "ronaTimeout": "20",
    "convIvrTranscript": "true",
    "customerRegion": "Country",
    "dnis": "+10000000001",
    "mohFileName": "default_moh.wav",
    "QueueId": "d2eddc63-5b32-4bb9-b7eb-8606e15b0992",
    "workflowId": "229ac95a-0294-4846-b7ff-681d4b784b27"
  },
  "callFlowParams": {
    "config": {
      "dtmfTerminatorSymbol": "#",
      "persistTranscript": "true",
      "noInputTimeout": "5",
      "inputLanguage": "en-US",
      "outputVoice": "en-US-Standard-A",
      "volumeGain": "0.0",
      "dtmfTimeout": "5",
      "bargeIn": "true",
      "terminationDelay": "5",
      "maxNoInputCount": "3",
      "speakingRate": "1.0"
    }
  },
  "isTerminated": false,
  "contactDirection": {
    "type": "INBOUND"
  },
  "currentVTeam": "d2eddc63-5b32-4bb9-b7eb-8606e15b0992",
  "previousVTeams": [
    "87005d40-11c3-47bb-840c-05621716205f"
  ],
  "isFcManaged": true,
  "outboundType": null,
  "workflowManager": null,
  "queuedTimestamp": null,
  "createdTimestamp": 1700000000000,
  "mediaProperties": null,
  "mainInteractionId": "66a872f1-8502-44ef-a71d-d8867374bfa0",
  "parentInteractionId": "66a872f1-8502-44ef-a71d-d8867374bfa0",
  "isMediaForked": false,
  "flowProperties": null,
  "segmentParticipants": null
}
```

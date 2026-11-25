---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentChannelStateChanged
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentChannelStateChanged
This is triggered when the state of a specific agent channel type changes, commonly after a successful state change request or other channel-related state updates.

> This event is applicable for agents using the v2 login and v2 state-change flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                                      | **Description**                                                                                     |
|------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| `channelType`                                  | Channel type whose state changed. Example values: `telephony`, `chat`, `email`, `social`.           |
| `agentChannelStateDetail`                      | State details for the channel type included in this notification.                                    |
| `agentChannelStateDetail.agentState`           | Current state of the channel. Example values: `Available`, `Idle`, `WrapUp`.                        |
| `agentChannelStateDetail.availableChannelCount` | Number of available channels for this channel type after the state change.                           |
| `agentChannelStateDetail.totalChannelCount`    | Total configured channel count for this channel type.                                                |
| `agentChannelStateDetail.stateChangeReason`    | Reason associated with the channel state change, when available.                                     |
| `agentChannelStateDetail.manuallyAssignedChannelCount` | Number of manually assigned channels currently available for this channel type.                      |
| `agentChannelStateDetail.totalManuallyAssignedChannelCount` | Total manually assigned channel count configured for this channel type.                              |
| `agentChannelStateDetail.pendingIdle`          | Indicates whether the channel is waiting to move to idle after active work completes.                |
| `agentChannelStateDetail.stateChangeTimestamp` | Time when the channel state changed, in epoch milliseconds.                                          |
| `agentChannelStateDetail.auxCodeId`            | Auxiliary code associated with the channel state, when available.                                    |
| `agentChannelStateDetail.lastIdleCodeChangeTimestamp` | Time when the idle/aux code last changed for the channel, in epoch milliseconds, when available.     |
| `connectedChannels`                            | List of connected channel identifiers associated with the agent after the state change.              |
| `changedById`                                  | Identifier of the user who initiated the state change, when available.                               |
| `changedBy`                                    | Indicates who initiated the state change, when available. Example values: `SELF`, `SUPERVISOR`.      |
| `changedByName`                                | Display name of the user who initiated the state change, when available.                             |
| `status`                                       | Agent status after the channel state change. Example value: `LoggedIn`.                             |
| `isClientInitiated`                            | Indicates whether the channel state change was initiated by a client request.                        |
| `subStatus`                                    | Agent sub-status after the channel state change. Example values: `Available`, `Idle`.                |
| `isAgentLogin`                                 | Indicates whether this notification was generated as part of agent login, when available.            |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "7b23f5d9-8d3a-4a19-9a24-2f6a3e8d1b55",
  "orgId": "3e8c7a21-5b94-4d6f-9c71-8a2f0e6d4b33",
  "channelType": "telephony",
  "agentChannelStateDetail": {
    "agentState": "WrapUp",
    "availableChannelCount": 0,
    "totalChannelCount": 1,
    "stateChangeReason": "",
    "manuallyAssignedChannelCount": 0,
    "totalManuallyAssignedChannelCount": 0,
    "pendingIdle": false,
    "stateChangeTimestamp": 1779295823024,
    "auxCodeId": "",
    "lastIdleCodeChangeTimestamp": 1779292272544
  },
  "agentSessionId": "b6e9c2f1-1c5d-45a2-8f41-0d2a4e7c9b66",
  "trackingId": "d5a9f7c4-6e2b-4f18-b8d2-9c3a1e5f7b90",
  "connectedChannels": [
    "4d7e8b1a-2c93-4f6d-9a51-8e3b0c6f2d44"
  ],
  "changedById": null,
  "changedBy": null,
  "queueId": "9c1b2e4f-6a73-4d80-95b2-1e7f3a9c5d88",
  "changedByName": null,
  "status": "LoggedIn",
  "isClientInitiated": false,
  "subStatus": "Available",
  "isAgentLogin": null,
  "eventTime": 1779295823027,
  "type": "AgentChannelStateChanged"
}
```

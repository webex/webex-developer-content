---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentChannelReloginSuccess
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentChannelReloginSuccess
This is triggered when a reload request succeeds for a session established with V2 behavior and the agent channel session state is restored. It can follow either a V1 or V2 reload request because the success event is selected from the persisted login-session version.

> This event is applicable to sessions established with V2 behavior. Reloading the agent does not change the session version.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                                                | **Description**                                                                                         |
|----------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| `dn`                                                     | Agent dial number or WebRTC endpoint used for voice handling.                                            |
| `siteId`                                                 | Site identifier currently associated with the agent.                                                     |
| `teamId`                                                 | Team identifier currently associated with the agent.                                                     |
| `interactionIds`                                         | List of interaction identifiers currently linked to the restored agent session, if any.                  |
| `profileType`                                            | Agent profile type. Example values: `BLENDED`, `BLENDED_REAL_TIME`, `EXCLUSIVE`.                        |
| `channelsMap`                                            | Channel-type to channel-ID mapping for the restored agent session.                                       |
| `agentChannelStateDetailMap`                             | Channel-type to channel-state-detail mapping for the restored agent session.                             |
| `agentChannelStateDetailMap.<channelType>.agentState`    | Current state for the channel type. Example values: `Available`, `Idle`, `WrapUp`.                      |
| `agentChannelStateDetailMap.<channelType>.availableChannelCount` | Number of available channels for the channel type after reload.                                          |
| `agentChannelStateDetailMap.<channelType>.totalChannelCount` | Total configured channel count for the channel type.                                                     |
| `agentChannelStateDetailMap.<channelType>.stateChangeReason` | Reason associated with the latest channel state change, when available.                                  |
| `agentChannelStateDetailMap.<channelType>.manuallyAssignedChannelCount` | Number of manually assigned channels currently available for the channel type.                           |
| `agentChannelStateDetailMap.<channelType>.totalManuallyAssignedChannelCount` | Total manually assigned channel count configured for the channel type.                                   |
| `agentChannelStateDetailMap.<channelType>.pendingIdle`   | Indicates whether the channel is waiting to move to idle after active work completes.                    |
| `agentChannelStateDetailMap.<channelType>.stateChangeTimestamp` | Time when the channel state changed, in epoch milliseconds.                                              |
| `agentChannelStateDetailMap.<channelType>.auxCodeId`     | Auxiliary code associated with the channel state, when available.                                        |
| `agentChannelStateDetailMap.<channelType>.lastIdleCodeChangeTimestamp` | Time when the idle/aux code last changed for the channel, in epoch milliseconds, when available.         |
| `isExtension`                                            | Indicates whether the restored voice login uses extension-based handling.                                |
| `roles`                                                  | Roles associated with the logged-in user. Example value: `agent`.                                        |
| `deviceType`                                             | Device type associated with the restored session, when available. Example value: `BROWSER`.              |
| `deviceId`                                               | Device identifier associated with the restored session, when available.                                  |
| `reservedAgentChannelIds`                                | Channel identifiers currently reserved for the agent, when available.                                    |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "7d3e0f6b-8a12-4c55-9ef0-2b7c6f9a4d31",
  "orgId": "1a9c4d72-6f85-4b0e-9c33-5e7a2d8f0b44",
  "dn": "web************************************4d31",
  "siteId": "5c8a7b1e-4d92-4e66-b4c7-2d9f6a1e0c73",
  "teamId": "8b2e6d91-3f47-4a8c-91b5-6e0d4c2f7a38",
  "interactionIds": [],
  "agentSessionId": "2f6c9a4b-3e81-45d0-9b7f-8a1c4e6d2b93",
  "trackingId": "9e4b7d2a-5c13-41f8-8a6e-3d0b9c5f7a21",
  "profileType": "BLENDED",
  "channelsMap": {
    "ma_telephony": [],
    "email": [],
    "telephony": [
      "6a5d2f91-8c37-4b0e-b7a2-1f9d4c6e3a85"
    ],
    "ma_chat": [],
    "chat": [],
    "customMessaging": [],
    "workItem": [],
    "ma_email": [],
    "ma_social": [],
    "ma_workItem": [],
    "ma_customMessaging": [],
    "social": []
  },
  "agentChannelStateDetailMap": {
    "telephony": {
      "agentState": "Idle",
      "availableChannelCount": 0,
      "totalChannelCount": 1,
      "stateChangeReason": "agent-wss-disconnect",
      "manuallyAssignedChannelCount": 0,
      "totalManuallyAssignedChannelCount": 0,
      "pendingIdle": false,
      "stateChangeTimestamp": 1779367777900,
      "auxCodeId": "4e9b1c6d-7a25-4f83-9d0e-6b2c5a8f1d44",
      "lastIdleCodeChangeTimestamp": 1779367777900
    }
  },
  "isExtension": false,
  "roles": [
    "agent"
  ],
  "deviceType": "BROWSER",
  "deviceId": "webrtc-7d3e0f6b-8a12-4c55-9ef0-2b7c6f9a4d31",
  "reservedAgentChannelIds": [],
  "eventTime": 1779367811322,
  "type": "AgentChannelReloginSuccess"
}
```

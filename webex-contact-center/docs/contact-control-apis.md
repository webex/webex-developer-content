---
type: Guide
title: Contact Control APIs
display_title: Contact Control APIs
canonical_url: https://developer.webex.com/docs/contact-control-apis
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/contact-control-apis)

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Asynchronous Contact Control APIs - Websocket Notification Payload Mappings

| **Rest API**                                                                       | **Websocket Notification**                                                                                                                                                                                                                                                                                                                                                                                                    |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Accept Preview Task](https://developer.webex.com/docs/api/v1/tasks-call-control/accept-preview-task)         | [CampaignPreviewAcceptFailed](https://developer.webex.com/docs/contact-control-apis#campaignpreviewacceptfailed)                                                                                                                                                                                                                                                                                                                                         |
| [Accept Task](https://developer.webex.com/docs/api/v1/tasks-call-control/accept-task)                         | [AgentContactAssigned](https://developer.webex.com/docs/contact-control-apis#agentcontactassigned)<br/>[AgentContactAssignFailed](https://developer.webex.com/docs/contact-control-apis#agentcontactassignfailed)                                                                                                                                                                                                                                                                   |
| [Buddy Agents List](https://developer.webex.com/docs/api/v1/agents/buddy-agents-list)                         | [BuddyAgents](https://developer.webex.com/docs/contact-control-apis#buddyagents)<br/>[BuddyAgentsRetrieveFailed](https://developer.webex.com/docs/contact-control-apis#buddyagentsretrievefailed)                                                                                                                                                                                                                                                                                   |
| [Conference Exit Task](https://developer.webex.com/docs/api/v1/tasks-call-control/conference-exit-task)       | [AgentConsultConferenceEnded](https://developer.webex.com/docs/contact-control-apis#agentconsultconferenceended)                                                                                                                                                                                                                                                                                                                                         |
| [Consult Conference Task](https://developer.webex.com/docs/api/v1/tasks-call-control/consult-conference-task) | [AgentConsultConferenced](https://developer.webex.com/docs/contact-control-apis#agentconsultconferenced)                                                                                                                                                                                                                                                                                                                                                 |
| [Consult End Task](https://developer.webex.com/docs/api/v1/tasks-call-control/consult-end-task)               | [AgentConsultEndFailed](https://developer.webex.com/docs/contact-control-apis#agentconsultendfailed)<br/>[AgentCtqCancelled](https://developer.webex.com/docs/contact-control-apis#agentctqcancelled)<br/>[AgentCtqCancelFailed](https://developer.webex.com/docs/contact-control-apis#agentctqcancelfailed)                                                                                                                                                                                                   |
| [Consult Task](https://developer.webex.com/docs/api/v1/tasks-call-control/consult-task)                       | [AgentConsultCreated](https://developer.webex.com/docs/contact-control-apis#agentconsultcreated)<br/>[AgentConsultFailed](https://developer.webex.com/docs/contact-control-apis#agentconsultfailed)<br/>[AgentConsulting](https://developer.webex.com/docs/contact-control-apis#agentconsulting)<br/>[AgentCtqFailed](https://developer.webex.com/docs/contact-control-apis#agentctqfailed)                                                                                                                                               |
| [Consult Transfer Task](https://developer.webex.com/docs/api/v1/tasks-call-control/consult-transfer-task)     | [AgentConsultTransferred](https://developer.webex.com/docs/contact-control-apis#agentconsulttransferred)<br/>[AgentConsultTransferFailed](https://developer.webex.com/docs/contact-control-apis#agentconsulttransferfailed)                                                                                                                                                                                                                                                         |
| [End Task](https://developer.webex.com/docs/api/v1/tasks-call-control/end-task)                               | [ContactEnded](https://developer.webex.com/docs/contact-control-apis#contactended)                                                                                                                                                                                                                                                                                                                                                                       |
| [Hold Task](https://developer.webex.com/docs/api/v1/tasks-call-control/hold-task)                             | [AgentContactHeld](https://developer.webex.com/docs/contact-control-apis#agentcontactheld)<br/>[AgentContactHoldFailed](https://developer.webex.com/docs/contact-control-apis#agentcontactholdfailed)                                                                                                                                                                                                                                                                               |
| [Login](https://developer.webex.com/docs/api/v1/agents/login)                                                 | [AgentStationLoginSuccess](https://developer.webex.com/docs/contact-control-apis#agentstationloginsuccess)<br/>[AgentStationLoginFailed](https://developer.webex.com/docs/contact-control-apis#agentstationloginfailed)                                                                                                                                                                                                                                                             |
| [Logout](https://developer.webex.com/docs/api/v1/agents/logout)                                               | [AgentLogoutSuccess](https://developer.webex.com/docs/contact-control-apis#agentlogoutsuccess)<br/>[AgentLogoutFailed](https://developer.webex.com/docs/contact-control-apis#agentlogoutfailed)                                                                                                                                                                                                                                                                                     |
| [Pause Recording](https://developer.webex.com/docs/api/v1/tasks-call-control/pause-recording-task)            | [ContactRecordingPaused](https://developer.webex.com/docs/contact-control-apis#contactrecordingpaused)<br/>[ContactRecordingPauseFailed](https://developer.webex.com/docs/contact-control-apis#contactrecordingpausefailed)                                                                                                                                                                                                                                                         |
| [Pause Task](https://developer.webex.com/docs/api/v1/tasks-call-control/pause-task)                          | [AgentContactPaused](https://developer.webex.com/docs/contact-control-apis#agentcontactpaused)<br/>[AgentContactPauseFailed](https://developer.webex.com/docs/contact-control-apis#agentcontactpausefailed)                                                                                                                                                                                                                                                                         |
| [Reload (V1)](https://developer.webex.com/docs/api/v1/agents/reload)<br/>[Reload (V2)](https://developer.webex.com/docs/api/v2/agents/reload) | [AgentReloginSuccess](https://developer.webex.com/docs/contact-control-apis#agentreloginsuccess)<br/>[AgentContact](https://developer.webex.com/docs/contact-control-apis#agentcontact)<br/>[AgentChannelReloginSuccess](https://developer.webex.com/docs/contact-control-apis#agentchannelreloginsuccess)                                                                                                                                                                                                     |
| [Remove Preview Task](https://developer.webex.com/docs/api/v1/tasks-call-control/resume-preview-task)         | [CampaignPreviewRemoveFailed](https://developer.webex.com/docs/contact-control-apis#campaignpreviewremovefailed)                                                                                                                                                                                                                                                                                                                                         |
| [Resume Recording](https://developer.webex.com/docs/api/v1/tasks-call-control/resume-recording-task)          | [ContactRecordingResumed](https://developer.webex.com/docs/contact-control-apis#contactrecordingresumed)<br/>[ContactRecordingResumeFailed](https://developer.webex.com/docs/contact-control-apis#contactrecordingresumefailed)                                                                                                                                                                                                                                                     |
| [Resume Task](https://developer.webex.com/docs/api/v1/tasks-call-control/resume-task)                        | [AgentContactResumed](https://developer.webex.com/docs/contact-control-apis#agentcontactresumed)<br/>[AgentContactResumeFailed](https://developer.webex.com/docs/contact-control-apis#agentcontactresumefailed)                                                                                                                                                                                                                                                                     |
| [Skip Preview Task](https://developer.webex.com/docs/api/v1/tasks-call-control/skip-preview-task)             | [CampaingnPreviewSkipFailed](https://developer.webex.com/docs/contact-control-apis#campaignpreviewskipfail)                                                                                                                                                                                                                                                                                                                                              |
| [State Change](https://developer.webex.com/docs/api/v1/agents/state-change)                                   | [AgentStateChangeSuccess](https://developer.webex.com/docs/contact-control-apis#agentstatechangesuccess)<br/>[AgentStateChangeFailed](https://developer.webex.com/docs/contact-control-apis#agentstatechangefailed)<br/>[AgentChannelStateChanged](https://developer.webex.com/docs/contact-control-apis#agentchannelstatechanged)<br/>[AgentChannelStateChangeFailed](https://developer.webex.com/docs/contact-control-apis#agentchannelstatechangefailed)                                                                                                                                              |
| [Transfer Task](https://developer.webex.com/docs/api/v1/tasks-call-control/transfer-task)                     | [AgentBlindTransferred](https://developer.webex.com/docs/contact-control-apis#agentblindtransferred)<br/>[AgentBlindTransferFailed](https://developer.webex.com/docs/contact-control-apis#agentblindtransferfailed)<br/>[AgentVteamTransferred](https://developer.webex.com/docs/contact-control-apis#agentvteamtransferred)<br/>[AgentVteamTransferFailed](https://developer.webex.com/docs/contact-control-apis#agentvteamtransferfailed)<br/>[AgentBlindTransferFailedEvent](https://developer.webex.com/docs/contact-control-apis#agentblindtransferfailedevent) |
| [Unhold Task](https://developer.webex.com/docs/api/v1/tasks-call-control/unhold-task)                         | [AgentContactUnheld](https://developer.webex.com/docs/contact-control-apis#agentcontactunheld)<br/>[AgentContactUnHoldFailed](https://developer.webex.com/docs/contact-control-apis#agentcontactunholdfailed)                                                                                                                                                                                                                                                                       |
| [Wrap Up Task](https://developer.webex.com/docs/api/v1/tasks-call-control/wrap-up-task)                       | [AgentWrapup](https://developer.webex.com/docs/contact-control-apis#agentwrapup)<br/>[AgentWrappedUp](https://developer.webex.com/docs/contact-control-apis#agentwrappedup)                                                                                                                                                                                                                                                                                                         |

### Reload session version behavior

The reload success event and restored state format depend on the API version persisted when the agent logged in, not on the reload endpoint version. The active session remains on its login version until the agent logs out and starts a new session.

| **Persisted login-session version** | **Reload endpoint**                         | **Success event**                                                                    | **Session version after reload** |
|-------------------------------------|---------------------------------------------|--------------------------------------------------------------------------------------|----------------------------------|
| V1                                  | [V1](https://developer.webex.com/docs/api/v1/agents/reload)            | [AgentReloginSuccess](#agentreloginsuccess)                                           | V1                               |
| V1                                  | [V2](https://developer.webex.com/docs/api/v2/agents/reload)            | [AgentReloginSuccess](#agentreloginsuccess)                                           | V1                               |
| V2                                  | [V1](https://developer.webex.com/docs/api/v1/agents/reload)            | [AgentChannelReloginSuccess](#agentchannelreloginsuccess)                             | V2                               |
| V2                                  | [V2](https://developer.webex.com/docs/api/v2/agents/reload)            | [AgentChannelReloginSuccess](#agentchannelreloginsuccess)                             | V2                               |

Use the `agentSessionId` and `interactionIds` returned in reload notifications to restore client-side session and interaction context. These identifiers describe restored backend context; they do not independently guarantee continuity of a client-managed voice or WebRTC media connection.

## Registering for Websocket Connection

To register a websocket connection in order to receive notifications during operations like Login, Logout, State Change and Reload use the following API:

Note: All events sent over the websocket are related to the specific agent/supervisor currently logged in.

- [Subscribe to Web Socket Notifications for Contact Control](https://developer.webex.com/docs/api/v1/notification/subscribe-notification)

## Common Payload Fields

The following fields appear across many notification payloads and keep the same general meaning wherever they are used.

| **Field**         | **Description**                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------|
| `eventType`       | Top-level category of the notification payload.                                                                |
| `type`            | Specific notification event name for the payload.                                                              |
| `orgId`           | Unique identifier of the organization associated with the event.                                               |
| `agentId`         | Unique identifier of the agent associated with the event, when applicable.                                     |
| `interactionId`   | Unique identifier of the interaction associated with the event, when applicable.                               |
| `interaction`     | Interaction details associated with the event. Refer to [Interaction](https://developer.webex.com/docs/contact-control-apis#interaction). |
| `queueMgr`        | Queue manager associated with the event, when applicable.                                                      |
| `mediaResourceId` | Identifier of the media resource associated with the event, when applicable.                                   |
| `trackingId`      | Unique identifier used to trace the request or event flow across systems.                                      |
| `eventTime`       | Time at which the event occurred, in epoch milliseconds.                                                       |
| `agentSessionId`  | Unique identifier of the active agent session associated with the event, when applicable.                      |
| `queueId`         | Unique identifier of the queue associated with the event, when applicable.                                     |

## Possible Notification Payloads Received

## AgentAddCampaignReservation

This is triggered when an agent is reserved for an outbound call that is generated by the campaign manager.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**          | **Description**                                                                                                                                            |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`       | Unique identifier of the dialer campaign associated with the reservation.                                                                                  |
| `agentChannelId`   | Unique identifier of the agent channel on which the reservation is created.                                                                                |
| `mediaType`        | Media channel of the interaction. Example value: `telephony`.                                                                                              |

</details>

```json
{
  "type": "AgentAddCampaignReservation",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "aqm",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "agentChannelId": "agent-channel-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "mediaType": "telephony",
  "eventTime": 1700000000000
}
```
## AgentBlindTransferFailed
This is triggered when a blind transfer to another participant fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Unique identifier of the destination agent to whom the transfer was attempted.                                                                             |
| `destinationType` | Type of the transfer destination. Example values: `Agent`,`DN`,`EP-DN`.                                                                                    |
| `reason`          | Failure reason returned for blind transfer failure. Example values: `MEDIA_MANAGER_INTERNAL_ERROR`, `INVALID_CONTACT_STATE`                                |
| `reasonCode`      | Numeric code associated with the failure reason. Example values: `136`(MEDIA_MANAGER_INTERNAL_ERROR),`108`(INVALID_CONTACT_STATE)                          |

</details>

```json
{
  "type": "AgentBlindTransferFailed",
  "eventType": "RoutingMessage",
  "interactionId": "0fa1d0dd-9ece-48a3-a7dd-80dd12730444",
  "mediaResourceId": "0fa1d0dd-9ece-48a3-a7dd-80dd12730444",
  "orgId": "2f342cf9-178b-46d1-ba54-35adda6e36d2",
  "queueMgr": "dummy-queue-manager",
  "agentId": "001e9881-c04c-4a70-bace-1445f750b71c",
  "destAgentId": "54f0d7e3-938e-4b59-8be8-b0e40fb43b36",
  "interaction": {...},
  "destinationType": "Agent",
  "reason": "MEDIA_MANAGER_INTERNAL_ERROR",
  "reasonCode": 136,
  "trackingId": "ed55a956-1d97-43d8-a309-4686166e3af9"
}
```

## AgentBlindTransferFailedEvent
This is triggered when a blind transfer fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                               |
|-------------------|---------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Unique identifier of the destination agent to whom the blind transfer was attempted.                          |
| `reason`          | Failure reason returned on why the blind transfer failed. Example values:`CONTACT_NOT_FOUND`                  |
| `reasonCode`      | Numeric code associated with the failure reason. Example values:`1042` (CONTACT_NOT_FOUND).                   |
| `destinationType` | Type of the transfer destination. Example values:`Agent`,`DN`,`EP-DN`.                                        |

</details>

```json
{
  "eventType": "RoutingMessage",
  "interactionId": "cfaac3d5-8e1a-4fc4-80a0-3d604f273987",
  "orgId": "73081463-94b9-4ace-bc6f-d597d1354bf1",
  "agentId": "7faa3405-cf82-4397-b64d-5bfee23ffc55",
  "destAgentId": "1ac430d9-70bd-4e89-97f8-a799d1572a87",
  "agentSessionId": "208b965f-4a7a-4f54-84c6-18bc838ad37d",
  "trackingId": "96ce9730-14e2-11ee-b8fa-537f253a2f1a",
  "reason": "CONTACT_NOT_FOUND",
  "reasonCode": 1042,
  "destinationType": "Agent",
  "eventTime": 1687867392081,
  "type": "AgentBlindTransferFailedEvent"
}
```

## AgentBlindTransferred
This is triggered when a blind transfer to another participant is successful.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Unique identifier of the destination agent to whom the contact was blind transferred.                                                                      |
| `destinationType` | Type of the transfer destination. Example vales: `Agent`,`DN`,`EP-DN`.                                                                                      |

</details>

```json
{
  "type": "AgentBlindTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "0fa1d0dd-9ece-48a3-a7dd-80dd12730444",
  "orgId": "2f342cf9-178b-46d1-ba54-35adda6e36d2",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "0fa1d0dd-9ece-48a3-a7dd-80dd12730444",
  "agentId": "001e9881-c04c-4a70-bace-1445f750b71c",
  "destAgentId": "54f0d7e3-938e-4b59-8be8-b0e40fb43b36",
  "interaction": {...},
  "destinationType": "Agent",
  "trackingId": "ed55a956-1d97-43d8-a309-4686166e3af9"
}
```

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

## AgentChannelState
This is triggered to reflect the latest state of an agent’s channel after a contact-related update.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                          |
|-------------------|------------------------------------------------------------------------------------------|
| `channelId`       | Unique identifier of the agent channel whose current state is being reported.            |
| `subStatus`       | Latest sub-status for the channel after the update. Example values: `Available`, `Idle`. |
| `wrapupAuxCodeId` | Wrap-up code associated with the channel state update, when applicable.                  |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "agentId": "agent-id-1",
  "agentSessionId": "agent-session-id-1",
  "channelId": "channel-id-1",
  "subStatus": "Available",
  "wrapupAuxCodeId": "wrapup-aux-code-id-1",
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "AgentChannelState"
}
```

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

## AgentChannelStateChangeFailed
This is triggered when a state change request for a specific agent channel type fails.

> This event is applicable for agents using the v2 login and v2 state-change flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**     | **Description**                                                                            |
|---------------|--------------------------------------------------------------------------------------------|
| `channelType` | Channel type for which the state change failed. Example values: `telephony`, `chat`, `email`, `social`. |
| `reason`      | Failure reason returned for the channel state change request.                              |
| `reasonCode`  | Numeric code associated with the failure reason.                                           |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "7b23f5d9-8d3a-4a19-9a24-2f6a3e8d1b55",
  "orgId": "3e8c7a21-5b94-4d6f-9c71-8a2f0e6d4b33",
  "channelType": "telephony",
  "reason": "INVALID_AGENT_STATE",
  "reasonCode": 1001,
  "trackingId": "d5a9f7c4-6e2b-4f18-b8d2-9c3a1e5f7b90",
  "eventTime": 1779295823027,
  "type": "AgentChannelStateChangeFailed"
}
```

## AgentConferenceTransferred
This is triggered when conference ownership is handed off to a new participant, typically after the primary agent leaves a conference interaction and a new owner is selected.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**           | **Description**                                                                                                                            |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`       | Identifier of the destination participant that became the new conference owner.                                                           |
| `destinationType`   | Type of destination participant that received the conference transfer. Example values: `Agent`, `DN`.                                    |
| `sourceDn`          | Source dial number associated with the transfer, when available.                                                                           |

</details>

```json
{
  "type": "AgentConferenceTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "mediaResourceId": "media-resource-id-1",
  "agentId": "agent-id-1",
  "destAgentId": "agent-id-2",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "destinationType": "Agent",
  "sourceDn": "source-dn-1",
  "eventTime": 1700000000000
}
```

## AgentConsultConferenced
This is triggered when a consult call is successfully converted to a conference..

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                       |
|--------------------------|-------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg that was joined into the conference.        |
| `destAgentId`            | Identifier of the consult destination joined into the conference. In the example, this is a DN value. |
| `destinationType`        | Type of the conference destination. Example values: `Agent`,`DN`,`EP-DN`.                             |

</details>

```json
{
  "type": "AgentConsultConferenced",
  "eventType": "RoutingMessage",
  "interactionId": "bc1386ae-ad41-4900-89d1-553fd4010b62",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "bc1386ae-ad41-4900-89d1-553fd4010b62",
  "consultMediaResourceId": "d0bcbd38-881f-4d3f-9c77-67f2f0c5d20c",
  "agentId": "d9090e8b-a35d-46bd-9171-2923acaeefda",
  "destAgentId": "2147651221",
  "interaction": {...},
  "trackingId": "5b6679ad-064b-49f0-a647-9fdd2b978735",
  "destinationType": "DN"
}
```

## AgentConsultConferenceEnded
This is triggered when a consult conference ends successfully.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                     |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg that exited or ended from the conference.                                 |
| `destAgentId`            | Unique identifier of the consult participant associated with the conference end event. In the example, this is an agent identifier. |
| `destinationType`        | Type of the conference participant destination. Example values:`Agent`,`DN`,`EP-DN`.                                                |
| `force`                  | Boolean flag indicating whether the conference exit/end was forced. Example values:`false`,`true`.                                  |

</details>

```json
{
  "type": "AgentConsultConferenceEnded",
  "eventType": "RoutingMessage",
  "interactionId": "d9164514-aaab-4220-bbfd-457ff844e279",
  "orgId": "d5284d60-7175-4700-a692-9d861ad3d589",
  "queueMgr": "dummy-queue-manager",
  "consultMediaResourceId": "consult_CSRVZRQN2T4KZ2KB",
  "agentId": "29d67c88-751b-40fb-9672-34f73549c89e",
  "destAgentId": "e98147f3-9f1b-4baf-9062-96584ba31766",
  "interaction": {...},
  "trackingId": "7d5259bb-c3f7-468d-8d72-a7dfa3458e72",
  "destinationType": "Agent",
  "force": false,
  "eventTime": 1687870870115
}
```

## AgentConsultConferencing
This is triggered in consult-to-EP-DN conferencing flows when an agent starts conferencing the consult interaction, and the conferencing update is sent for the parent interaction context.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                    | **Description**                                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `conferencedParticipantId`   | Identifier of the participant being added into the conference.                                                                             |
| `conferencedParticipantType` | Type of participant being added into the conference. Example values: `EP-DN`, `AGENT`.                                                     |

</details>

```json
{
  "type": "AgentConsultConferencing",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "agentId": "agent-id-1",
  "queueMgr": "queue-manager-1",
  "mediaResourceId": "media-resource-id-1",
  "interaction": {...},
  "conferencedParticipantId": "consult-party-id-1",
  "conferencedParticipantType": "EP-DN",
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## AgentConsultCreated
This is triggered when a consult interaction is created successfully.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the newly created consult leg.                                                                                   |
| `destAgentId`            | Unique identifier of the intended consult destination. In the example, this is another agent identifier.                                                   |
| `destinationType`        | Type of the consult destination. Example values: `Agent`,`DN`,`EP-DN`.                                                                                      |

</details>

```json
{
  "type": "AgentConsultCreated",
  "eventType": "RoutingMessage",
  "interactionId": "6e54dd0f-9da5-4ac6-b56b-a2e3657bbb9f",
  "orgId": "348adfa2-b8f0-405c-a516-da004eefde5f",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "6e54dd0f-9da5-4ac6-b56b-a2e3657bbb9f",
  "consultMediaResourceId": "da957aa2-dfb1-429e-aa5a-a216c874ca38",
  "agentId": "f8373b22-8c29-4e94-8ff6-aa52e50d1a18",
  "destAgentId": "0346a971-acf1-41b0-bb63-c1861e120d30",
  "interaction": {...},
  "trackingId": "c5348bdc-76ff-44c8-9684-7b7a41612656",
  "destinationType": "Agent"
}
```

## AgentConsultEndFailed
This event is triggered when an attempt to end a consult fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg that the system attempted to end.                                                                |
| `destAgentId`            | Identifier of the consult destination associated with the consult leg being ended. In the example, this is a DN value.                                     |
| `reason`                 | Failure reason returned on why the consult end attempt failed. Example values: `MEDIA_MANAGER_PRECONDITION_FAILED`.                                        |
| `reasonCode`             | Numeric code associated with the failure reason. Example values: `142` (Bad Request).                                                                      |

</details>

```json
{
  "type": "AgentConsultEndFailed",
  "eventType": "RoutingMessage",
  "interactionId": "dc0704cc-4e17-4b1a-944e-9d5e86f87b84",
  "orgId": "f222e3af-1a53-42ef-9deb-7520034b8a10",
  "queueMgr": "dummy-queue-manager",
  "consultMediaResourceId": "8e7ae556-3f22-4839-b949-4fcadff7c9d5",
  "agentId": "16839506-7c48-4a71-ba1b-d585e5d37607",
  "destAgentId": "9997770103",
  "interaction": {...},
  "reason": "MEDIA_MANAGER_PRECONDITION_FAILED",
  "reasonCode": 142,
  "trackingId": "cbdd4a89-b4ee-429d-a86d-72855f6a03b9"
}
```

## AgentConsultFailed
This is triggered when an attempt to start a consult fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Unique identifier of the intended consult destination. In the example, this is another agent identifier.                                                   |
| `reason`          | Failure reason returned on why the consult attempt failed. Example values `NO_MATCHING_AGENT_CHANNEL_FOUND`.                                               |
| `reasonCode`      | Numeric code associated with the failure reason. Example values: `1046`(NO_MATCHING_AGENT_CHANNEL_FOUND).                                                  |
| `destinationType` | Type of the consult destination. Example values: `Agent`,`DN`,`EP-DN`.                                                                                     |

</details>

```json
{
  "type": "AgentConsultFailed",
  "eventType": "RoutingMessage",
  "interactionId": "1f1ccfde-58a9-4f8f-8f8c-d12cd1ac3319",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "queueMgr": "dummy-queue-manager",
  "agentId": "109332be-7fc4-4d4d-9488-ebdb8e13b9bb",
  "destAgentId": "7c4ac9cf-014d-4e09-9e1f-d26b13704fdc",
  "interaction": {...},
  "reason": "NO_MATCHING_AGENT_CHANNEL_FOUND",
  "reasonCode": 1046,
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7",
  "destinationType": "Agent"
}
```

## AgentConsulting
This is triggered when the interaction enters the consulting state.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg while the interaction is in the consulting state. |
| `destAgentId`            | Unique identifier of the consult destination. In the example, this is another agent identifier.             |
| `destinationType`        | Type of the consult destination. Example values: `Agent`,`DN`,`EP-DN`.                                      |

</details>

```json
{
  "type": "AgentConsulting",
  "eventType": "RoutingMessage",
  "interactionId": "d9af7d2f-cb72-4abc-974e-5484594a1c67",
  "orgId": "348adfa2-b8f0-405c-a516-da004eefde5f",
  "queueMgr": "dummy-queue-manager",
  "consultMediaResourceId": "36a854fe-86c3-42f1-9f2c-1b46ea4409da",
  "agentId": "32247eed-2b46-4b9d-a99b-9b8ba35bdc66",
  "destAgentId": "a6aa9e25-eef4-4711-a62a-a9d846916995",
  "interaction": {...},
  "trackingId": "e0c13af6-85a4-48ec-b657-b4bb1a348177",
  "destinationType": "Agent"
}
```

## AgentConsultTransferFailed
This is triggered when a consult transfer to another participant fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                            |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId` | Media resource identifier associated with the consult leg created during the consult transfer flow.                                                        |
| `destAgentId`            | Identifier of the intended transfer destination. In the example, this is a DN value rather than an agent UUID.                                             |
| `reason`                 | Failure reason returned on why the consult transfer failed. Example values: `OPERATION_DISALLOWED_FOR_INTERACTION_STATE`.                                  |
| `reasonCode`             | Numeric code associated with the failure reason. Example values: `1089` (OPERATION_DISALLOWED_FOR_INTERACTION_STATE).                                      |
| `destinationType`        | Type of the transfer destination. Example values:`Agent`,`DN`,`EP-DN`.                                                                                     |

</details>

```json
{
  "type": "AgentConsultTransferFailed",
  "eventType": "RoutingMessage",
  "interactionId": "dc0704cc-4e17-4b1a-944e-9d5e86f87b84",
  "orgId": "f222e3af-1a53-42ef-9deb-7520034b8a10",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "dc0704cc-4e17-4b1a-944e-9d5e86f87b84",
  "consultMediaResourceId": "8e7ae556-3f22-4839-b949-4fcadff7c9d5",
  "agentId": "16839506-7c48-4a71-ba1b-d585e5d37607",
  "destAgentId": "9997770103",
  "interaction": {...},
  "reason": "OPERATION_DISALLOWED_FOR_INTERACTION_STATE",
  "reasonCode": 1089,
  "trackingId": "cbdd4a89-b4ee-429d-a86d-72855f6a03b9",
  "destinationType": "DN"
}
```

## AgentConsultTransferred
This is triggered when a consult transfer to another participant is successful.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                    | **Description**                                                                                                     |
|------------------------------|---------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId`     | Media resource identifier associated with the consult leg created during the consult transfer flow.                 |
| `transferredMediaResourceId` | Media resource identifier for the consult leg that becomes the transferred leg after the consult transfer succeeds. |
| `destAgentId`                | Unique identifier of the destination agent to whom the consult transfer was completed.                              |
| `destinationType`            | Type of the transfer destination. Example values: `Agent`,`DN`,`EP-DN`.                                             |

</details>

```json
{
  "type": "AgentConsultTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "93b1212f-9a62-43a4-ac32-a91e544f02c5",
  "orgId": "d5e3a633-13a6-47b1-93cb-fa0dc2cf9717",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "93b1212f-9a62-43a4-ac32-a91e544f02c5",
  "consultMediaResourceId": "e4081e22-03e4-40c5-9c3e-66016b9659bd",
  "transferredMediaResourceId": "e4081e22-03e4-40c5-9c3e-66016b9659bd",
  "agentId": "95c05c44-8c16-425a-9abb-959329291f23",
  "destAgentId": "0cdbef6d-af48-49d2-9167-398917261ca2",
  "interaction": {...},
  "trackingId": "7e992bc6-527b-4667-81dc-38f3ccc45b28",
  "destinationType": "Agent"
}
```

## AgentConsultTransferring
This is triggered in consult-to-EP-DN transfer flows when an agent starts transferring the consult interaction, and the transfer update is sent for the active interaction.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                    | **Description**                                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `transferredParticipantId`   | Identifier of the participant being transferred.                                                                                           |
| `transferredParticipantType` | Type of participant being transferred. Example values: `EP-DN`, `AGENT`.                                                                   |

</details>

```json
{
  "type": "AgentConsultTransferring",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "agentId": "agent-id-1",
  "queueMgr": "queue-manager-1",
  "mediaResourceId": "media-resource-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "transferredParticipantId": "consult-party-id-1",
  "transferredParticipantType": "EP-DN",
  "eventTime": 1700000000000
}
```

## AgentContact
This is triggered during agent reload/relogin recovery when contact details are fetched for active interactions already assigned to the agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| `isConsulted`            | Indicates whether the agent is joined as a consulted participant for this interaction.                                          |
| `consultMediaResourceId` | Media resource identifier for the consult leg, when available.                                                                  |
| `reservedAgentChannelId` | Reserved channel identifier for campaign reservation scenarios, when available.                                                 |

</details>

```json
{
  "type": "AgentContact",
  "eventType": "RoutingMessage",
  "interactionId": "5a3c1e9d-7b42-4f8a-9d6c-2e1f3a4b5c6d",
  "orgId": "1f2e3d4c-5b6a-4a8d-9c1e-7b2a3c4d5e6f",
  "queueMgr": "queue-manager",
  "agentId": "9c7d6e5f-3a2b-4f8d-8e1c-0b9a7d6e5f4c",
  "isConsulted": false,
  "mediaResourceId": "6e5d4c3b-2a1f-4e8d-9c0b-3a2b1c4d5e6f",
  "consultMediaResourceId": null,
  "interaction": {...},
  "trackingId": "2b3c4d5e-6f7a-4a8d-b9c1-3e2f1a4b5c6d",
  "reservedAgentChannelId": null,
  "eventTime": 1700000013000
}
```

## AgentContactAssigned
This is triggered when a contact is successfully assigned to an agent and is ready to be handled, across both inbound and outbound interaction flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                  | **Description**                                                                                                                                                     |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationInteractionId` | Optional reservation interaction identifier for campaign/reservation flows.                                                                                         |
| `campaignReservationKey`   | Optional campaign reservation key for outbound campaign flows.                                                                                                      |
| `agentEmailId`             | Optional agent email identifier when available.                                                                                                                     |

</details>

```json
{
  "type": "AgentContactAssigned",
  "eventType": "RoutingMessage",
  "interactionId": "a8814c56-4ad6-46e3-97a7-b073e51158dc",
  "orgId": "4594f7c7-a526-4be6-b6f1-1c752ea75917",
  "queueMgr": "queue-manager",
  "mediaResourceId": "a18e6b3a-e0c1-4bc3-8d38-c1cf9dc33acd",
  "agentId": "343fac6e-bb8a-4c3e-9c94-92201af01f20",
  "interaction": {...},
  "trackingId": "11cc09b9-cecb-4063-b3ac-eb2f762341b9",
  "eventTime": 1700000000000,
  "reservationInteractionId": null,
  "campaignReservationKey": null,
  "agentEmailId": "agent@example.com"
}
```

## AgentContactAssignFailed
This is triggered when a contact assignment to an agent fails across inbound or outbound interaction flows.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                  | **Description**                                                                                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`                   | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`.                    |
| `reasonCode`               | Numeric code associated with the failure reason. Example values: `1011` (participant add failed), `1012` (agent already found), `1010` (participant invite timeout). |
| `reservationInteractionId` | Optional reservation interaction identifier for campaign/reservation flows.                                                                                          |
| `campaignReservationKey`   | Optional campaign reservation key for outbound campaign flows.                                                                                                       |
| `agentEmailId`             | Optional agent email identifier when available.                                                                                                                      |

</details>

```json
{
  "type": "AgentContactAssignedFailed",
  "eventType": "RoutingMessage",
  "interactionId": "92e61c7b-fa90-448b-ac51-078fea52c39e",
  "orgId": "13241ad0-31f0-4c71-87ad-75a9859b3b7d",
  "queueMgr": "queue-manager",
  "mediaResourceId": "74fb6da2-de46-4f2f-90ec-41f8a63c092f",
  "agentId": "8a3f681a-9c61-4dcf-a14e-69329759a094",
  "interaction": {...},
  "reason": "USER_DECLINED",
  "reasonCode": 156,
  "trackingId": "98377bd0-9d12-4330-8552-163ec9cb46b7",
  "eventTime": 1700000000000,
  "reservationInteractionId": null,
  "campaignReservationKey": null,
  "agentEmailId": "agent@example.com"
}
```

## AgentContactEndFailed
This is triggered when an attempt to end the contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`          | Failure reason returned on why the contact end attempt failed. Example values: `INVALID_CHAT_STATUS`.                                                      |
| `reasonCode`      | Numeric code associated with the failure reason. Example values: `150`(INVALID_CHAT_STATUS).                                                               |

</details>

```json
{
  "type": "AgentContactEndFailed",
  "eventType": "RoutingMessage",
  "interactionId": "7aeefb07-0c79-46bf-9c1b-d558201855b0",
  "orgId": "b333ee78-8263-4370-a60a-967182fc91e4",
  "queueMgr": "dummy-queue-manager",
  "mediaResourceId": "CSR0X8VPA0O3PDXX",
  "agentId": "0bf99cb3-faa8-4f3f-abd4-a171776c424a",
  "interaction": {...},
  "reason": "INVALID_CHAT_STATUS",
  "reasonCode": 150,
  "trackingId": "0ccd89f2-639f-445c-a987-02dc1515aed6",
  "eventTime": 1687846566263
}
```

## AgentContactHeld
This is triggered when an active contact is successfully placed on hold by an agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Description**                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId` - Optional destination agent identifier for consult or transfer scenarios, when applicable.                                                                       |

</details>

```json
{
  "type": "AgentContactHeld",
  "eventType": "RoutingMessage",
  "interactionId": "7d2491bc-0dae-4c73-8969-f642d590b703",
  "orgId": "2e78188d-2c0d-4c2a-9408-9bd7436095c7",
  "queueMgr": "queue-manager",
  "mediaResourceId": "25deaac7-dd61-42aa-a165-c2124f7a326a",
  "agentId": "3ab74c76-4651-4c8c-9a47-0ca60a716680",
  "interaction": {...},
  "trackingId": "2895e095-a03e-4dd7-8332-7c1cad64a64f",
  "destAgentId": "a74b5306-c898-46b6-9546-cee687286aea",
  "eventTime": 1700000002000
}
```

## AgentContactHoldFailed
This is triggered when an attempt to place an active contact on hold fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Description**                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason` - Failure reason returned for the hold attempt. Example values: `USER_LEFT`, `MEDIA_APP_SERVER_ERROR`.                                                                 |
| `reasonCode` - Numeric code associated with the failure reason. Example values: 105 (user left), 138 (media app server error).                                                  |

</details>

```json
{
  "type": "AgentContactHoldFailed",
  "eventType": "RoutingMessage",
  "interactionId": "e7098133-41fb-48ec-8fa1-103f7baef3f8",
  "orgId": "548205a6-bba5-49da-9cfa-c69ea9280fd1",
  "queueMgr": "queue-manager",
  "mediaResourceId": "daa7142b-44b4-453d-a054-0a4d904c9795",
  "agentId": "ce892125-7f8d-467f-b4ef-6b8f9ef7f4b9",
  "interaction": {...},
  "reason": "USER_LEFT",
  "reasonCode": 105,
  "trackingId": "a981de59-a646-4573-8fa7-f2eab7ab6854",
  "eventTime": 1700000000000
}
```

## AgentContactPaused
This is triggered when an active non-real-time digital contact is successfully paused by an agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentContactPaused",
  "eventType": "RoutingMessage",
  "interactionId": "fcb4d956-2e50-4ee3-b82d-4a131d196499",
  "orgId": "6f07de7d-c5e8-4ab3-a065-3a5c4c2df07d",
  "interaction": {...},
  "agentId": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "trackingId": "0f0ba862-a191-49b1-96b8-63409b79c813",
  "eventTime": 1700000000000
}
```

## AgentContactPauseFailed
This is triggered when an attempt to pause a contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the pause attempt. Example values: `ALLOWED_PAUSED_CONTACTS_LIMIT_EXCEEDED`, `INTERACTION_NOT_ASSIGNED_TO_AGENT`.                                  |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1113` (`ALLOWED_PAUSED_CONTACTS_LIMIT_EXCEEDED`), `1045` (`INTERACTION_NOT_ASSIGNED_TO_AGENT`).               |

</details>

```json
{
  "type": "AgentContactPauseFailed",
  "eventType": "RoutingMessage",
  "interactionId": "fcb4d956-2e50-4ee3-b82d-4a131d196499",
  "orgId": "6f07de7d-c5e8-4ab3-a065-3a5c4c2df07d",
  "interaction": {...},
  "agentId": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "reason": "ALLOWED_PAUSED_CONTACTS_LIMIT_EXCEEDED",
  "reasonCode": 1113,
  "trackingId": "0f0ba862-a191-49b1-96b8-63409b79c813",
  "eventTime": 1700000000000
}
```

## AgentContactResumed
This is triggered when a paused contact is successfully assigned again.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                   | **Description**                                                                                                                                                                                                                                              |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `assignedAgentIdBeforePause` | Unique identifier of the agent assigned to the contact before it was paused.                                                                                                                                                                                  |
| `resumedBy.type`            | Identifies who resumed the contact. Supported values are `RESUMED_BY_AGENT`, `RESUMED_BY_SUPERVISOR`, and `RESUMED_BY_SYSTEM`.                                                                                                                                |
| `resumeReason.type`         | Identifies why the contact resumed. Supported values are `RESUME_REASON_MANUAL`, `RESUME_REASON_PAUSE_TIMEOUT`, and `RESUME_REASON_CUSTOMER_REPLY`.                                                                                                           |

</details>

```json
{
  "type": "AgentContactResumed",
  "eventType": "RoutingMessage",
  "interactionId": "fcb4d956-2e50-4ee3-b82d-4a131d196499",
  "orgId": "6f07de7d-c5e8-4ab3-a065-3a5c4c2df07d",
  "interaction": {...},
  "agentId": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "assignedAgentIdBeforePause": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "resumedBy": {
    "type": "RESUMED_BY_AGENT"
  },
  "resumeReason": {
    "type": "RESUME_REASON_MANUAL"
  },
  "trackingId": "0f0ba862-a191-49b1-96b8-63409b79c813",
  "eventTime": 1700000000000
}
```

## AgentContactResumeFailed
This is triggered when an attempt to resume a paused contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                                                            |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the resume attempt. Example values: `OPERATION_DISALLOWED_FOR_INTERACTION_STATE`, `INVALID_USER_ROLE`, `INSUFFICIENT_PERMISSION`.                                               |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1089` (`OPERATION_DISALLOWED_FOR_INTERACTION_STATE`), `1092` (`INVALID_USER_ROLE`), `1060` (`INSUFFICIENT_PERMISSION`).                      |

</details>

```json
{
  "type": "AgentContactResumeFailed",
  "eventType": "RoutingMessage",
  "interactionId": "fcb4d956-2e50-4ee3-b82d-4a131d196499",
  "orgId": "6f07de7d-c5e8-4ab3-a065-3a5c4c2df07d",
  "interaction": {...},
  "agentId": "90870b5b-d459-4e0b-8e83-fcdd87532598",
  "reason": "OPERATION_DISALLOWED_FOR_INTERACTION_STATE",
  "reasonCode": 1089,
  "trackingId": "0f0ba862-a191-49b1-96b8-63409b79c813",
  "eventTime": 1700000000000
}
```

## AgentContactUnassigned
This is triggered when a contact is unassigned from an agent during routing or transfer handling.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`          | Optional reason returned for the unassignment event.                                                                                                       |
| `reasonCode`      | Optional numeric code associated with the reason.                                                                                                          |

</details>

```json
{
  "type": "AgentContactUnassigned",
  "eventType": "RoutingMessage",
  "interactionId": "542f0d71-ca8d-4cc6-82e6-9e8fa913dc11",
  "orgId": "d93976e7-d3f0-45d2-b885-e7db5dfb98d6",
  "queueMgr": "queue-manager",
  "mediaResourceId": "2517a2ec-742e-4890-8c7f-42232ff05974",
  "agentId": "89d4d02f-b481-4606-a273-2ecc7cdd9439",
  "interaction": {...},
  "trackingId": "c9753b26-f9ce-4f5f-9d6e-bb97598980a6",
  "reason": null,
  "reasonCode": null,
  "eventTime": 1700000010000
}
```

## AgentContactUnheld
This is triggered when a held contact is successfully resumed by an agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                                    |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destAgentId`     | Optional destination agent identifier for consult or transfer scenarios.                                                                                           |

</details>

```json
{
  "type": "AgentContactUnheld",
  "eventType": "RoutingMessage",
  "interactionId": "8fad4d0b-60a5-4a7a-970a-762879694911",
  "orgId": "fad72201-9c4d-45fc-9c18-7d293930e581",
  "queueMgr": "queue-manager",
  "mediaResourceId": "c41d8ad5-c985-4cb4-9093-f419ea1e9ab0",
  "agentId": "8a9e031c-331f-45e8-97f7-c1dc0bf6ad79",
  "interaction": {...},
  "trackingId": "40b603bc-8ae1-4073-8c42-5a9b20662eb4",
  "destAgentId": null,
  "eventTime": 1700000003000
}
```

## AgentContactUnHoldFailed
This is triggered when an attempt to unhold a contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`          | Failure reason returned for the unhold attempt. Example values: `USER_LEFT`.                                                                               |
| `reasonCode`      | Numeric code associated with the failure reason. Example values: 105 (user left).                                                                          |

</details>

```json
{
  "type": "AgentContactUnHoldFailed",
  "eventType": "RoutingMessage",
  "interactionId": "47162758-76dc-4b21-ad45-548547d64f2c",
  "orgId": "0c8ea9ac-8882-42e0-b9d2-06e74009d08b",
  "queueMgr": "queue-manager",
  "mediaResourceId": "110c821c-5ecf-4f8d-ac9c-c55cdc12494a",
  "agentId": "d1e9cf5d-c473-4d0b-82f8-2f779aca0b0e",
  "interaction": {...},
  "reason": "USER_LEFT",
  "reasonCode": 105,
  "trackingId": "979f3da9-c55b-448f-a5d5-98b605d5f6d4",
  "eventTime": 1700000004000
}
```

## AgentCtqCancelFailed
This is triggered when an attempt to cancel a consult-to-queue request fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned on why the consult-to-queue cancel request failed. Example values: `CHILD_CONTACT_NOT_FOUND`.                                      |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1047` (CHILD_CONTACT_NOT_FOUND).                                                         |

</details>

```json
{
  "type": "AgentCtqCancelFailed",
  "eventType": "RoutingMessage",
  "interactionId": "1f1ccfde-58a9-4f8f-8f8c-d12cd1ac3319",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "queueMgr": "dummy-queue-manager",
  "agentId": "109332be-7fc4-4d4d-9488-ebdb8e13b9bb",
  "queueId": "7c4ac9cf-014d-4e09-9e1f-d26b13704fdc",
  "interaction": {...},
  "reason": "CHILD_CONTACT_NOT_FOUND",
  "reasonCode": 1047,
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7"
}
```

## AgentCtqCancelled
This is triggered when a consult-to-queue request is cancelled successfully.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentCtqCancelled",
  "eventType": "RoutingMessage",
  "interactionId": "1f1ccfde-58a9-4f8f-8f8c-d12cd1ac3319",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "queueMgr": "dummy-queue-manager",
  "agentId": "109332be-7fc4-4d4d-9488-ebdb8e13b9bb",
  "queueId": "7c4ac9cf-014d-4e09-9e1f-d26b13704fdc",
  "interaction": {...},
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7"
}
```

## AgentCtqFailed
This is triggered when a consult-to-queue request fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned on why the consult-to-queue request failed. Example values:`MaxWaitTimeInQueueExceeded`.                                           |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1049` (MaxWaitTimeInQueueExceeded).                                                      |

</details>

```json
{
  "type": "AgentCtqFailed",
  "eventType": "RoutingMessage",
  "interactionId": "e3a50cbc-e494-4207-abe7-34ff92f0713b",
  "orgId": "4df9bd96-7288-44a1-9f1c-40e2038d35b0",
  "queueMgr": "dummy-queue-manager",
  "agentId": "7fd8d46c-8224-4704-89b2-7baa2824fcdf",
  "queueId": "c7d713bd-4dcc-4a28-b8c6-89b7dd0f8fb4",
  "interaction": {...},
  "reason": "MaxWaitTimeInQueueExceeded",
  "reasonCode": 1049,
  "trackingId": "dc177520-12a6-11ee-8eb2-fd656a256ad2",
  "eventTime": 1687622436306
}
```

## AgentDNRegistered
This is triggered when an agent's dial number (DN) is successfully registered for contact handling.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**     | **Description**                                                                   |
|---------------|-----------------------------------------------------------------------------------|
| `dn`          | Dial number that was registered for the agent.                                    |
| `isExtension` | Indicates whether the registered DN is an extension.                              |
| `mediaMgr`    | Media manager that processed the DN registration. Example values: `vmm`,`callmm`. |

</details>

```json
{
  "type": "AgentDNRegistered",
  "eventType": "RoutingMessage",
  "agentId": "8fadc403-9ab3-4722-a30e-9cab5f295587",
  "orgId": "1e00dd80-24ab-4bf1-aaf0-06db94af683f",
  "dn": "555***5074",
  "trackingId": "ad8c4597-11b1-44c3-9e0d-ada919720f5f",
  "isExtension": false,
  "mediaMgr": "vmm",
  "eventTime": 1768998476190
}
```

## AgentDNRegisterFailure
This is triggered when an agent DN registration request fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned on why the DN registration failed. Example values: `DUPLICATE_LOCATION`.     |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `127` (`DUPLICATE_LOCATION`).       |
| `mediaMgr`   | Media manager that processed the DN registration request. Example values: `vmm`,`callmm`.            |

</details>

```json
{
  "type": "AgentDNRegisterFailure",
  "eventType": "RoutingMessage",
  "agentId": "efd60e0a-51b3-4926-b4c4-bb040b9788f8",
  "orgId": "c0a54e64-768f-4541-b747-eec09e225252",
  "reason": "DUPLICATE_LOCATION",
  "reasonCode": 127,
  "trackingId": "25bffd46-4b67-4a70-85ee-5e8f71ced1ff",
  "mediaMgr": "callmm",
  "eventTime": 1768984253850
}
```

## AgentInviteFailed
This is triggered when an attempt to invite an agent fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**        | **Description**                                                                                                                                 |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`         | Failure reason returned on why the invite failed.                                                                                               |
| `reasonCode`     | Numeric code associated with the failure reason.                                                                                                |
| `agentType`      | Type/category of the invited agent.                                                                                                             |

</details>

```json
{
  "type": "AgentInviteFailed",
  "eventType": "RoutingMessage",
  "interactionId": "4e7d2c91-8f3b-4c5a-9a61-2b8d7e1c6f40",
  "orgId": "9b6f2a4d-3c8e-4a71-b5d9-0f1e7c8a2643",
  "queueMgr": "dummy_qm",
  "agentId": "2a6c8f5e-4b91-4d73-9e20-7c3b1d5a648f",
  "interaction": {...},
  "reason": "DUMMY_REASON",
  "reasonCode": 0,
  "trackingId": "3f7b9d2e-6c4a-4f51-8e90-1a2c5b6d7f48",
  "agentType": "Dummy",
  "eventTime": 0,
  "agentSessionId": "8c5a7d2f-4e91-4b63-9f20-1d6e3a9c748b"
}
```

## AgentLogoutFailed
This is triggered when an agent logout request fails due to validation, state, or session constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the logout attempt. Example value: `AGENT_HAS_ASSIGNED_CONTACTS`.                   |
| `reasonCode` | Numeric code associated with the failure reason. Example value: `1039` for assigned contacts preventing logout. |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentLogoutFailed",
  "agentId": "7b3b351e-c49f-4cf4-93c4-fddc3b6a6e98",
  "orgId": "0670b522-6ffe-48a9-b7a0-9f4d0f5b8644",
  "reason": "AGENT_HAS_ASSIGNED_CONTACTS",
  "reasonCode": 1039,
  "trackingId": "76c64852-79a5-4410-9172-87479b9d9f93",
  "eventTime": 1774343932852
}
```

## AgentLogoutSuccess
This is triggered when an agent logout request is successfully completed and the session is closed.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                   |
|-------------------|-----------------------------------------------------------------------------------|
| `status`          | Agent status after logout (for example, `LoggedOut`).                             |
| `subStatus`       | Agent sub-status at logout completion (for example, `Idle`).                      |
| `loggedOutBy`     | Actor that initiated the logout. Example values: `MACHINE`, `SELF`, `SUPERVISOR`. |
| `roles`           | Roles associated with the user for this logout event.                             |
| `logoutReason`    | Logout reason.                                                                    |
| `wrapupAuxCodeId` | Wrap-up auxiliary code identifier associated with logout, when available.         |
</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentLogoutSuccess",
  "agentId": "5c6f12a9-39ce-4867-9031-1123783d4ca1",
  "orgId": "84ff943d-11b3-4a4f-9fa1-ec75bc0be2e7",
  "status": "LoggedOut",
  "subStatus": "Idle",
  "agentSessionId": "b2ed5c84-cd20-4fe5-8063-b7f14020dedb",
  "loggedOutBy": "SELF",
  "trackingId": "d70f305c-4f51-4315-ad81-13bddfb99ace",
  "roles": ["agent"],
  "logoutReason": "Agent Logged Out",
  "wrapupAuxCodeId": null,
  "eventTime": 1774336757816
}
```

## AgentManualAssignContactFailed
This is triggered when a manual contact assignment request to an agent fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                               |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned on why the manual assignment failed. Example values: `OPERATION_DISALLOWED_FOR_INTERACTION_STATE`.   |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1089` (`OPERATION_DISALLOWED_FOR_INTERACTION_STATE`).      |

</details>

```json
{
  "type": "AgentManualAssignContactFailed",
  "eventType": "RoutingMessage",
  "interactionId": "7a4c9e2b-3d6f-4a81-9b50-1e7c5d8a204f",
  "orgId": "c6b8a4e1-9d3f-4b72-8a50-2e7c1d5f904a",
  "agentId": "e9b1c7a4-6d3f-4a82-9c50-7e2d1b5a904b",
  "reason": "OPERATION_DISALLOWED_FOR_INTERACTION_STATE",
  "reasonCode": 1089,
  "trackingId": "2d7c5a9e-4b1f-4e83-9a50-6c8d1b7f904c",
  "eventTime": 1768917624823
}
```

## AgentOfferCampaignReservation

This is triggered when an agent is offered for an outbound call that is generated by the campaign manager.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**          | **Description**                                                                                                                                            |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`       | Unique identifier of the dialer campaign associated with the offered reservation.                                                                          |
| `ronaTimeout`      | Ring-no-answer timeout, in seconds, for the agent to accept the offered reservation before RONA handling is triggered.                                     |
| `agentChannelId`   | Unique identifier of the agent channel on which the offer is presented.                                                                                    |

</details>

```json
{
  "type": "AgentOfferCampaignReservation",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "aqm",
  "mediaResourceId": "media-resource-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "ronaTimeout": 26,
  "agentChannelId": "agent-channel-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## AgentOfferConsult
This is triggered when a consult interaction is offered to the target agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**               | **Description**                                                                                                                                 |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `consultMediaResourceId`| Unique identifier of the consult media resource associated with the consult offer.                                                              |
| `consultingAgentId`     | Unique identifier of the agent who initiated the consult request.                                                                               |
| `ronaTimeout`           | Ring-no-answer timeout configured for the consult offer.                                                                                        |

</details>

```json
{
  "type": "AgentOfferConsult",
  "eventType": "RoutingMessage",
  "interactionId": "f1a6c9e2-4b7d-4e3f-9a82-1d6c8b5e2047",
  "orgId": "a9e5c4b7-2d8f-4c61-9b30-6e1d7a8f2054",
  "queueMgr": "dummy_qm",
  "consultMediaResourceId": "c6b2e9f1-8a4d-4c73-9f50-1e7d5b8a2049",
  "agentId": "d7e4a1c9-5b6f-4a82-9c30-2e8d1f6b2057",
  "consultingAgentId": "e2b8d6a9-7c5f-4e41-9a30-1f5d8c6b2048",
  "ronaTimeout": 0,
  "interaction": {...},
  "trackingId": "9c3d6a1e-8b4f-4a72-9d50-7e2c1b6a9050",
  "eventTime": 0
}
```

## AgentOfferContact
his is triggered when a contact is offered to an agent for handling.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                | **Description**                                                                                                                                                    |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ronaTimeout`            | Ring-no-answer timeout, in seconds, for the agent to accept the offered contact before RONA handling is triggered.                                                 |
| `agentEmailId`           | Email address or masked email identifier of the agent receiving the contact offer.                                                                                 |
| `contactAssignmentType`  | Indicates how the contact was assigned to the agent. Example value: `ACD`.                                                                                         |

</details>

```json
{
  "type": "AgentOfferContact",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "aqm",
  "mediaResourceId": "media-resource-id-1",
  "agentId": "agent-id-1",
  "ronaTimeout": 18,
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "agentEmailId": "a***@example.com",
  "contactAssignmentType": "ACD"
}
```
## AgentOfferContactRona
This is triggered when a contact offer times out due to RONA and is not accepted by the agent in time.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reasonCode`      | Numeric code associated with the RONA reason. Defaults to `121`.                                                                                           |
| `reason`          | Reason returned for the RONA event. Defaults to RONA_TIMER_EXPIRED.                                                                                        |

</details>

```json
{
  "type": "AgentOfferContactRona",
  "eventType": "RoutingMessage",
  "interactionId": "501d28f5-650c-4a15-87d5-31e572800751",
  "orgId": "bfc4707c-0f52-4607-9efd-582152e764e4",
  "queueMgr": "queue-manager",
  "mediaResourceId": "0066462b-ce70-4b13-b856-e793b659e34f",
  "agentId": "8c72b5f8-6af1-4930-8ac2-c416ff4cbb22",
  "interaction": {...},
  "trackingId": "f46d8f6f-d45d-4d8b-b3b8-2f50a8e6bc64",
  "reasonCode": 121,
  "reason": "RONA_TIMER_EXPIRED",
  "eventTime": 1700000005000,
  "agentSessionId": "8ff66b12-917f-455c-a580-2e387b858ca9"
}
```

## AgentOutboundFailed
This is triggered when an outbound call attempt from an agent fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mediaType`     | Media channel of the interaction. Example value: `telephony`.                                                                                              |
| `reason`        | Failure reason returned for the outbound attempt. Example value: `AGENT_ENDS`.                                                                             |
| `reasonCode`    | Numeric code associated with the failure reason. Example value: `1024`.                                                                                    |

</details>

```json
{
  "type": "AgentOutboundFailed",
  "eventType": "RoutingMessage",
  "interactionId": "8c2f1a7e-5b49-4d3a-9e6c-3f7a1b4c8d93",
  "orgId": "8c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "agentId": "5c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "mediaType": "telephony",
  "queueId": "queue-id-1",
  "queueMgr": "aqm",
  "reason": "AGENT_ENDS",
  "reasonCode": 1024,
  "interaction": {...},
  "trackingId": "8c2f1a7e-6b49-4d3a-9e6c-2f7a1b4c8d93",
  "eventTime": 1700000000000
}
```
## AgentReloginFailed
This is triggered when an agent reload/relogin request fails because the current session state cannot be restored, such as when the agent or channel data cannot be fetched, the voice device is not ready, or reload is not allowed for the current session.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the relogin attempt. Example values: `AGENT_NOT_FOUND`, `AGENT_DN_NOT_REGISTERED`, `AGENT_CHANNEL_NOT_FOUND`, `AGENT_NOT_LOGGED_IN`, `INTERNAL_ERROR`.                                                                       |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1038` (agent not found), `1041` (DN not registered), `1027` (agent channel not found), `1059` (agent not logged in), `1037` (internal error), `36` (generic relogin failure fallback). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "5c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "orgId": "8c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "reason": "AGENT_NOT_FOUND",
  "reasonCode": 1038,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "AgentReloginFailed"
}
```

## AgentReloginSuccess
This is triggered when a reload request succeeds for a session established with V1 behavior and the current session state is restored. It can follow either a V1 or V2 reload request because the success event is selected from the persisted login-session version.

> This event is applicable to sessions established with V1 behavior. Reloading the agent does not change the session version.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                         |
|-------------------------------|-----------------------------------------------------------------------------------------|
| `status`                      | Agent status after reload (for example, `LoggedIn`).                                    |
| `subStatus`                   | Agent sub-status after reload (for example, `Idle`, `Available`).                       |
| `auxCodeId`                   | Auxiliary code associated with the current sub-status, when available.                  |
| `dn`                          | Agent dial number (station/extension) used for voice handling.                          |
| `siteId`                      | Site identifier currently associated with the agent.                                    |
| `teamId`                      | Team identifier currently associated with the agent.                                    |
| `interactionIds`              | List of interaction identifiers currently linked to the agent session, if any.          |
| `lastStateChangeTimestamp`    | Timestamp (epoch milliseconds) when the agent state last changed.                       |
| `lastStateChangeReason`       | Reason text associated with the most recent state change.                               |
| `lastIdleCodeChangeTimestamp` | Timestamp (epoch milliseconds) when the idle/aux code was last changed, when available. |
| `profileType`                 | Agent profile type. Possible values are BLENDED, BLENDED_REAL_TIME, EXCLUSIVE.          |
| `channelsMap`                 | Channel-type to channel-ID mapping for the agent.                                       |
| `isExtension`                 | Indicates whether the logged-in device is an extension-based login mode.                |
| `roles`                       | Roles associated with the logged-in user (for example, agent or supervisor).            |
| `deviceType`                  | Logged-in device type (if available).                                                   |
| `deviceId`                    | Logged-in device identifier (if available).                                             |
| `reservedAgentChannelIds`     | Channel identifiers that are currently reserved for the agent, when available.          |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentReloginSuccess",
  "agentId": "8c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "orgId": "1a7e9c3d-4b52-4f8a-b6c1-3d9e2f7a5b84",
  "status": "LoggedIn",
  "subStatus": "Idle",
  "auxCodeId": "6f3b2a9d-8c41-4e7a-b5d2-1c9e3a7f4b68",
  "dn": "web************************************3152",
  "siteId": "3d7a1c9e-5b42-4f6a-a8d1-2c7e9b3f5a64",
  "teamId": "9b4c2a7e-1d53-4f8a-b6c2-7e3a9d5f1b68",
  "interactionIds": [],
  "agentSessionId": "2e7a1c9d-5b43-4f8a-a6d1-3c9e7b2f5a64",
  "trackingId": "7a3c1e9d-4b52-4f8a-b6c1-2d9e5f7a3b68",
  "lastStateChangeTimestamp": 1774353178751,
  "lastStateChangeReason": "",
  "lastIdleCodeChangeTimestamp": 1774353178751,
  "profileType": "BLENDED",
  "channelsMap": {
    "telephony": ["4d7a1c9e-5b42-4f8a-a6d1-3c9e7b2f5a64"],
    "chat": [],
    "email": [],
    "social": [],
    "workItem": [],
    "customMessaging": [],
    "ma_telephony": [],
    "ma_chat": [],
    "ma_email": [],
    "ma_social": [],
    "ma_workItem": [],
    "ma_customMessaging": []
  },
  "isExtension": false,
  "roles": ["agent"],
  "eventTime": 1774353183985,
  "deviceType": "BROWSER",
  "deviceId": "webrtc-8c2f1a7e-5b49-4d3a-9e6c-2f7a1b4c8d93",
  "reservedAgentChannelIds": []
}
```

## AgentSkillsUpdate
This is triggered when an agent’s skills are updated after a skill profile or skill assignment change.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                 | **Description**                                                                       |
|---------------------------|---------------------------------------------------------------------------------------|
| `skillProfileId`          | Identifier of the skill profile currently associated with the agent, when applicable. |
| `skillProfileName`        | Name of the skill profile currently associated with the agent, when applicable.       |
| `skillProfileLevel`       | Level at which the skill profile is applied. Example values: `User`, `Team`.          |
| `skills`                  | List of skills currently associated with the agent after the update.                  |
| `skills[].skillId`        | Unique identifier of the skill.                                                       |
| `skills[].skillName`      | Display name of the skill.                                                            |
| `skills[].skillType`      | Type of skill value. Example values: `boolean`, `text`, `proficiency`, `enum`.        |
| `skills[].skillValue`     | Value currently assigned for the skill.                                               |
| `skills[].agentId`        | Unique identifier of the agent associated with the skill entry.                       |
| `skills[].isDynamicSkill` | Indicates whether the skill entry came from a dynamic skill assignment.               |
| `dialNumber`              | Agent dial number associated with the current session, when available.                |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "agentId": "agent-id-1",
  "trackingId": "tracking-id-1",
  "skillProfileId": "skill-profile-id-1",
  "skillProfileName": "Skill Profile Name",
  "skillProfileLevel": "User-level",
  "agentSessionId": "agent-session-id-1",
  "skills": [
    {
      "skillId": "skill-id-1",
      "skillName": "Skill Name 1",
      "skillType": "boolean",
      "skillValue": "1",
      "agentId": "agent-id-1",
      "isDynamicSkill": false
    },
    {
      "skillId": "skill-id-2",
      "skillName": "Skill Name 2",
      "skillType": "boolean",
      "skillValue": "1",
      "agentId": "agent-id-1",
      "isDynamicSkill": false
    }
  ],
  "dialNumber": "1000000000",
  "eventTime": 1700000000000,
  "type": "AgentSkillsUpdate"
}
```

## AgentStateChangeFailed
This is triggered when an agent state change request fails due to validation, state, or session constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                        |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `auxCodeId`  | Auxiliary code provided in the state change request.                                                                                                                   |
| `reason`     | Failure reason returned for the state change attempt. Example values: `STATE_CHANGE_DISALLOWED_IN_PENDING_LOGOUT`, `INVALID_STATE_CHANGE_REQUEST`, `AGENT_NOT_FOUND`.  |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1087` (pending logout restriction), `1074` (invalid state change request), `1038` (agent not found). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStateChangeFailed",
  "agentId": "6b1f9c3e-4a72-4d8e-b5c1-9f2a7e6c3d41",
  "orgId": "2c9e5a7d-8f41-4b63-a1d9-3e7c2b4f5a68",
  "auxCodeId": "9d3b7f21-6a5c-4e8d-92b1-c4f7a6e2d9b3",
  "reason": "STATE_CHANGE_DISALLOWED_IN_PENDING_LOGOUT",
  "reasonCode": 1087,
  "trackingId": "5e7a1c9d-3b42-4f8a-9d6c-1b2e3f4a5c7d",
  "eventTime": 1774349285638
}
```

## AgentStateChangeSuccess
This is triggered when an agent state change request is successfully applied.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                                                      |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `status`                      | Agent status after the state change. Example value: `LoggedIn`.                                                      |
| `subStatus`                   | Agent sub-status after the state change. Example values: `Idle`, `Available`.                                        |
| `auxCodeId`                   | Auxiliary code identifier associated with the updated sub-status.                                                    |
| `lastStateChangeTimestamp`    | Timestamp (epoch milliseconds) when the state was last changed.                                                      |
| `lastStateChangeReason`       | Reason text associated with the state change operation.                                                              |
| `lastIdleCodeChangeTimestamp` | Timestamp (epoch milliseconds) when the idle/aux code was last changed, if available.                                |
| `connectedChannels`           | Connected channel identifiers for the agent session.                                                                 |
| `changedById`                 | Unique Identifier of the user who initiated the state change, if available.                                          |
| `changedBy`                   | Source or actor that initiated the state change, if available. Example values: `SELF`, `SUPERVISOR`, `HELPDESK` etc. |
| `changedByName`               | Name of the user who initiated the state change, if available.                                                       |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStateChangeSuccess",
  "agentId": "aa0fb53e-736b-4be2-941d-24799292591b",
  "orgId": "689d8edf-3e5d-4e50-be99-59694b10ddde",
  "status": "LoggedIn",
  "subStatus": "Idle",
  "auxCodeId": "866eca53-d884-404a-b080-1ba336473d60",
  "agentSessionId": "1b6b84d0-ecba-45a5-94eb-2b22097b081d",
  "trackingId": "da62c8e1-baa8-45b7-8de9-65cc03987a7e",
  "lastStateChangeTimestamp": 1774349599073,
  "lastStateChangeReason": "",
  "lastIdleCodeChangeTimestamp": 1774349599073,
  "connectedChannels": [],
  "changedById": "aa0fb53e-736b-4be2-941d-24799292591b",
  "changedBy": "SELF",
  "changedByName": "************",
  "eventTime": 1774349599078
}
```

## AgentStationLoginFailed
This is triggered when an agent login request fails due to validation, state, or session constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                                                                                     |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the login attempt. Example values: `AGENT_SESSION_ALREADY_EXISTS`, `ALLOWED_AGENT_SESSION_LIMIT_EXCEEDED`, `AGENT_DN_EMPTY`, `DN_REGISTRATION_TIMEOUT`. |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `1035`(session exists) , `1019` (session limit exceded), `1036` (DN empty), `1058` (DN registration timeout).      |
</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStationLoginFailed",
  "agentId": "7ec529c3-8d13-4f95-a26b-14328517f340",
  "orgId": "9f97820b-d1d1-4e6b-b3eb-983af99aed57",
  "reason": "AGENT_SESSION_ALREADY_EXISTS",
  "reasonCode": 1035,
  "trackingId": "cc59c869-979c-40e9-a59f-93510602e7cc",
  "eventTime": 1774261973099
}
```

## AgentStationLoginSuccess
This is triggered when an agent login request is successfully completed.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                               |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| `status`                      | Agent status after login (for example, `LoggedIn`).                                           |
| `subStatus`                   | Agent sub-status after login (for example, `Idle` , `Available`).                             |
| `teamId`                      | Team identifier currently associated with the agent.                                          |
| `siteId`                      | Site identifier currently associated with the agent.                                          |
| `interactionIds`              | List of interaction identifiers currently linked to the agent session, if any.                |
| `auxCodeId`                   | Auxiliary code associated with the current sub-status, when available.                        |
| `chatCount`                   | Number of chat channels/capacity configured at login.                                         |
| `emailCount`                  | Number of email channels/capacity configured at login.                                        |
| `voiceCount`                  | Number of voice channels/capacity configured at login.                                        |
| `dn`                          | Agent dial number (station/extension) for voice handling.                                     |
| `channelsMap`                 | Channel-type to channel-ID mapping for the agent.                                             |
| `lastStateChangeTimestamp`    | Timestamp (epoch milliseconds) when the agent state last changed.                             |
| `lastIdleCodeChangeTimestamp` | Timestamp (epoch milliseconds) when the idle/aux code last changed, when available.           |
| `profileType`                 | Agent profile type. Possible values are BLENDED, BLENDED_REAL_TIME, EXCLUSIVE.                |
| `skills`                      | Skill list associated with the agent at login.                                                |
| `skillProfileId`              | Skill profile ID linked to the agent (if any).                                                |
| `skillProfileName`            | Skill profile display name linked to the agent (if any).                                      |
| `roles`                       | Roles associated with the logged-in user (for example, agent or supervisor).                  |
| `deviceType`                  | Logged-in device type (if available).                                                         |
| `deviceId`                    | Logged-in device identifier (if available).                                                   |
| `skillProfileLevel`           | Skill profile scope/level applied at login (for example, user-level or team-level).           |
| `agentStateControlEnabled`    | Indicates whether agent state control mode is enabled for this login session, when available. |
| `ciClientId`                  | Client identifier associated with the authenticated login session, when available.            |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "type": "AgentStationLoginSuccess",
  "agentId": "3f9c2b8e-7d4a-4f91-9c6b-1a2d5e8f0b12",
  "orgId": "a1b2c3d4-5e6f-47a8-9b0c-1d2e3f4a5b6c",
  "status": "LoggedIn",
  "subStatus": "Idle",
  "agentSessionId": "9c7d6e5f-4a3b-4c2d-8e1f-0a9b8c7d6e5f",
  "trackingId": "7a6b5c4d-3e2f-4a1b-9c8d-0e1f2a3b4c5d",
  "teamId": "d4c3b2a1-9f8e-47d6-b5c4-3a2f1e0d9c8b",
  "siteId": "f1e2d3c4-b5a6-47d8-9c0b-1a2e3d4c5b6f",
  "interactionIds": [],
  "auxCodeId": "c9b8a7d6-5e4f-47c3-b2a1-0d9e8f7a6b5c",
  "chatCount": 0,
  "emailCount": 0,
  "voiceCount": 1,
  "dn": "100001",
  "channelsMap": {
    "telephony": ["6e5d4c3b-2a1f-47e8-9d0c-1b2a3c4d5e6f"],
    "chat": [],
    "email": [],
    "social": [],
    "workItem": [],
    "customMessaging": [],
    "ma_telephony": [],
    "ma_chat": [],
    "ma_email": [],
    "ma_social": [],
    "ma_workItem": [],
    "ma_customMessaging": []
  },
  "lastStateChangeTimestamp": 1700000011000,
  "lastIdleCodeChangeTimestamp": 1700000011000,
  "profileType": "BLENDED",
  "skills": [],
  "skillProfileId": null,
  "skillProfileName": null,
  "roles": ["agent", "supervisor"],
  "eventTime": 1700000012000,
  "deviceType": "EXTENSION",
  "deviceId": "device-001",
  "skillProfileLevel": "Team-level",
  "agentStateControlEnabled": null,
  "ciClientId": "cb3a082c36da3cc6eabb59b75294c3ed522c8b7997a478b0db732f67e72b6805"
}
```

## AgentVteamTransferFailed
This is triggered when a transfer to a virtual team fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `vteamId`       | Unique identifier of the virtual team to which the transfer was attempted.                                                                                 |
| `vteamType`     | Type of the virtual team target. In the example, this is `inboundentrypoint`.                                                                              |
| `reason`        | Failure reason returned on why the virtual team transfer failed. Example values: `INVALID_CHAT_STATUS`.                                                    |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `150` (INVALID_CHAT_STATUS).                                                              |

</details>

```json
{
  "type": "AgentVteamTransferFailed",
  "eventType": "RoutingMessage",
  "interactionId": "b6f4b924-f7eb-467a-99b4-b20ad8f4975d",
  "orgId": "4df9bd96-7288-44a1-9f1c-40e2038d35b0",
  "queueMgr": "dummy-queue-manager",
  "agentId": "b25cddcc-1841-44ca-b60c-ad3eb0eef87d",
  "vteamId": "0d42888a-143b-4097-a095-4e12ba3d58f7",
  "vteamType": "inboundentrypoint",
  "reason": "INVALID_CHAT_STATUS",
  "reasonCode": 150,
  "interaction": {...},
  "trackingId": "6bc331d0-148e-11ee-a59f-75682fa22e5c",
  "eventTime": 1687831242160
}
```

## AgentVteamTransferred
This is triggered when a transfer to a virtual team is successful.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentVteamTransferred",
  "eventType": "RoutingMessage",
  "interactionId": "29729f46-6f11-40bb-8baa-023e3f9408ed",
  "orgId": "4df9bd96-7288-44a1-9f1c-40e2038d35b0",
  "agentId": "2ea10ee0-fdff-4e98-a98a-96609f0b4fa3",
  "queueMgr": "dummy-queue-manager",
  "interaction": {...},
  "trackingId": "fd10d955-cd2c-401b-a3bb-1de781852a8b",
  "eventTime": 1687869699460
}
```

## AgentWrappedUp
This is triggered when an agent completes wrap-up for a contact and the system records the wrap-up completion.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `wrapUpAuxCodeId` | Wrap-up code selected when wrap-up was completed, when available.                                                                                          |
| `agentChannelId`  | Agent channel identifier associated with the wrap-up completion, when available.                                                                           |

</details>

```json
{
  "type": "AgentWrappedUp",
  "eventType": "RoutingMessage",
  "interactionId": "88c8f520-fd53-43a2-94fc-7cebf502a361",
  "orgId": "2f342cf9-178b-46d1-ba54-35adda6e36d2",
  "queueMgr": "aqm",
  "agentId": "001e9881-c04c-4a70-bace-1445f750b71c",
  "interaction": {...},
  "trackingId": "3c01a470-2af8-11ed-b83c-0f912c34e136",
  "wrapUpAuxCodeId": "1fd4d25a-c745-4e73-9b44-9be37af6aa72"
}
```

## AgentWrapup
This is triggered when an agent is moved into wrap-up for a contact after the contact has ended.

For field details , refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "AgentWrapup",
  "eventType": "RoutingMessage",
  "interactionId": "5a7c2e91-3f4d-4b8a-9c12-6d8e1f0a7b33",
  "orgId": "8d1b6f3c-2a74-4e90-b5c8-9f3a2d7e6c11",
  "queueMgr": "aqm",
  "mediaResourceId": "c3e9a1b7-6d2f-4c88-a5e1-0b7d9f2c4a55",
  "agentId": "1f8c7a2d-9b3e-4d11-a6c4-5e2f7b9d8a66",
  "interaction": {...},
  "trackingId": "7b2d4e9c-1a6f-4c33-8d5e-2f9a7b6c1d88",
  "queueId": "e4c1a9d7-5b3f-4a66-9c21-8d7e2f1b0a44",
  "eventTime": 1776165847699
}
```

## BuddyAgents
This is triggered when a Buddy Agents List request is successfully processed and the matching buddy agent list is returned.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**               | **Description**                                                             |
|-------------------------|-----------------------------------------------------------------------------|
| `agentList`             | List of buddy agents that match the request filters (team/state/channel).   |
| `agentList[].agentId`   | Unique identifier of the buddy agent.                                       |
| `agentList[].agentName` | Display name of the buddy agent.                                            |
| `agentList[].siteId`    | Site identifier associated with the buddy agent.                            |
| `agentList[].teamId`    | Team identifier associated with the buddy agent.                            |
| `agentList[].dn`        | Buddy agent dial number (when available).                                   |
| `agentList[].state`     | Current state shown for the buddy agent (for example, `Available`, `Idle`). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "59195cc8-6e7a-41bf-af7f-b60ca8395225",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7",
  "agentList": [
    {
      "agentId": "59195cc8-6e7a-41bf-af7f-b60ca8395225",
      "agentName": "digitalmm-e2e-user1 d",
      "siteId": "96c8ddab-29da-4ff2-a701-bc28c9f52f76",
      "teamId": "59ce6eba-d6b7-4bdc-b38d-8b17eafa4458",
      "dn": "55163",
      "state": "Available"
    }
  ],
  "agentSessionId": "5b6679ad-064b-49f0-a647-9fdd2b978735",
  "type": "BuddyAgents"
}
```

## BuddyAgentsRetrieveFailed
This is triggered when a Buddy Agents List request fails due to validation, data retrieval, or internal processing constraints.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned for the buddy list request. Example values: `BUDDY_AGENTS_RETRIEVE_FAILED`.   |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `35` (buddy agents retrieve failed). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "agentId": "59195cc8-6e7a-41bf-af7f-b60ca8395225",
  "orgId": "bde75a64-f4d5-4ffc-a239-feb607c17ef8",
  "trackingId": "f82cd0a2-973d-4cd3-9e86-01a3a2410cd7",
  "reason": "BUDDY_AGENTS_RETRIEVE_FAILED",
  "reasonCode": 35,
  "type": "BuddyAgentsRetrieveFailed"
}
```

## CampaignAgentReserved
This is triggered when an agent is successfully reserved to handle a campaign call.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                                                                                   |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`                  | Unique identifier of the dialer campaign.                                                                                                         |
| `agentChannelId`              | Unique identifier for the channel associated with this agent and campaign.                                                                        |
| `mediaType`                   | Type of media in used on this campaign.                                                                                                           |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "agentSessionId": "agent-session-id-1",
  "agentChannelId": "agent-channel-id-1",
  "mediaType": "telephony",
  "queueId": "queue-id-1",
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "CampaignAgentReserved"
}
```

## CampaignAgentUnreserved
This is triggered when an agent is unreserved from a campaign call reservation.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                     | **Description**                                                                                                                                   |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`                  | Unique identifier of the dialer campaign.                                                                                                         |
| `agentChannelId`              | Unique identifier for the channel associated with this agent and campaign.                                                                        |
| `mediaType`                   | Type of media in used on this campaign.                                                                                                           |
| `reason`                      | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`. |
| `reservationEndInteractionId` | Unique identifier for the contact lifecycle associated with the reservation, which terminated.                                                    |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "agentSessionId": "agent-session-id-1",
  "agentChannelId": "agent-channel-id-1",
  "mediaType": "telephony",
  "queueId": "queue-id-1",
  "trackingId": "tracking-id-1",
  "reason": "AGENT_ENDS",
  "reservationEndInteractionId": null,
  "eventTime": 1700000000000,
  "type": "CampaignAgentUnreserved"
}
```

## CampaignPreviewAcceptFailed
This is triggered when an agent’s preview accept request cannot be completed for a preview campaign contact.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                                      |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`    | Unique identifier of the dialer campaign.                                                                                                                            |
| `reason`        | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`.                    |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1011` (participant add failed), `1012` (agent already found), `1010` (participant invite timeout). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "interactionId": "interaction-id-1",
  "reason": "INTERNAL_ERROR",
  "reasonCode": 1000,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "CampaignPreviewAcceptFailed"
}
```

## CampaignPreviewRemoveFailed
This is triggered when a remove action cannot be completed for the agent’s current preview campaign contact.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                                      |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`    | Unique identifier of the dialer campaign.                                                                                                                            |
| `reason`        | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`.                    |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1011` (participant add failed), `1012` (agent already found), `1010` (participant invite timeout). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "interactionId": "interaction-id-1",
  "reason": "INTERNAL_ERROR",
  "reasonCode": 1000,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "CampaignPreviewRemoveFailed"
}
```

## CampaignPreviewSkipFailed
This is triggered when a skip action cannot be completed for the agent’s current preview campaign contact.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                                      |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `campaignId`    | Unique identifier of the dialer campaign.                                                                                                                            |
| `reason`        | Failure reason returned for the assignment attempt. Example values: `PARTICIPANT_ADD_FAILED`, `AGENT_ALREADY_FOUND`,`PARTICIPANT_INVITE_TIMEOUT`.                    |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1011` (participant add failed), `1012` (agent already found), `1010` (participant invite timeout). |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "campaignId": "campaign-id-1",
  "agentId": "agent-id-1",
  "interactionId": "interaction-id-1",
  "reason": "INTERNAL_ERROR",
  "reasonCode": 1000,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000,
  "type": "CampaignPreviewSkipFailed"
}
```

## ContactCallbackFailed
This is triggered when a callback attempt for a contact fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**          | **Description**                                                                         |
|--------------------|-----------------------------------------------------------------------------------------|
| `terminatingParty` | Entity that caused the callback attempt to terminate. Example values: `Agent`.          |
| `reason`           | Failure reason returned on why the callback failed. Example values: `AGENT_ENDS`.       |
| `reasonCode`       | Numeric code associated with the failure reason. Example values: `1000` (`AGENT_ENDS`). |

</details>

```json
{
  "type": "ContactCallbackFailed",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "agentId": "agent-id-1",
  "queueId": "queue-id-1",
  "terminatingParty": "Agent",
  "reason": "AGENT_ENDS",
  "reasonCode": 1000,
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## ContactEnded
This is triggered when an active contact ends.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**             | **Description**                                                                                                                                                      |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `agentsPendingWrapUp` | List of agents who still have wrap-up work pending after the contact ended, when applicable.                                                                         |
| `terminatingParty`    | Participant that caused the contact to end. Example values: `Agent`, `Customer`, `System`.                                                                           |
| `reason`              | End reason associated with the contact termination. Example values: `Customer Left`, `AGENT_LEFT`, `SYSTEM_ERROR`.                                                   |
| `agentEmailId`        | Agent email identifier associated with the contact, when available.                                                                                                  |

</details>

```json
{
  "type": "ContactEnded",
  "eventType": "RoutingMessage",
  "interactionId": "3b1e9f6a-8c44-4b0e-a2d7-5c6a9f2d1e73",
  "orgId": "7f2c5d91-3a6e-4f89-b2c4-1e8d9a7b6c55",
  "queueMgr": "aqm",
  "mediaResourceId": "9a4d7c12-5b8e-4f3c-a1d9-6e2b7f8c0d44",
  "interaction": {...},
  "trackingId": "c6e1a9b4-2d7f-4c88-9a11-3f5d6e7b8c22",
  "agentsPendingWrapUp": [
    "d2b7f3c8-6e4a-4a91-8c3d-9f2b6e1a7c55"
  ],
  "terminatingParty": "Customer",
  "reason": "Customer Left",
  "eventTime": 1776160552810,
  "agentEmailId": "*************************"
}
```

## ContactOwnerChanged
This is triggered when contact ownership is transferred from one owner to another—such as during conference participant removal or similar handoff scenarios—and the updated interaction is then routed to the new assigned agent.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                            |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `fromOwner`       | Identifier of the previous owner of the contact.                                                                                           |
| `toOwner`         | Identifier of the new owner of the contact.                                                                                                |

</details>

```json
{
  "type": "ContactOwnerChanged",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "fromOwner": "agent-id-1",
  "toOwner": "agent-id-2",
  "mediaResourceId": "media-resource-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## ContactRecordingPaused
This is triggered when contact recording is successfully paused for an active interaction.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "ContactRecordingPaused",
  "eventType": "RoutingMessage",
  "interactionId": "1769efd7-229b-4544-b142-ffefcf4acc1e",
  "orgId": "d6897f60-25a7-43fa-9334-e83e0b101974",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "trackingId": "76fd02e4-0cdf-4762-998a-24ca48283c8b",
  "eventTime": 1700000006000
}
```

## ContactRecordingPauseFailed
This is triggered when an attempt to pause contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned for the pause request. Example values: `MEDIA_MANAGER_INTERNAL_ERROR`.                                                             |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `136` (media manager error).                                                              |

</details>

```json
{
  "type": "ContactRecordingPauseFailed",
  "eventType": "RoutingMessage",
  "interactionId": "021b02cf-202c-4259-8e49-8eef066f6bce",
  "orgId": "f9a9dd69-1187-4240-8f26-285030e86bf7",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "reason": "UNSUPPORTED_OPERATION_FOR_MEDIATYPE",
  "reasonCode": 162,
  "trackingId": "521ccc55-f94a-4378-93c1-81226134eb80",
  "eventTime": 1700000007000
}
```

## ContactRecordingResumed
This is triggered when contact recording is successfully resumed for an active interaction.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `autoResumed`   | Indicates whether the recording was resumed automatically.                                                                                                 |

</details>

```json
{
  "type": "ContactRecordingResumed",
  "eventType": "RoutingMessage",
  "interactionId": "cdd8f523-d93a-4e7d-910f-1358ac89af35",
  "orgId": "0daafeaf-be86-4363-b7f7-e4adae722cac",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "trackingId": "87008868-1069-4c3c-82b9-eceaa3027314",
  "autoResumed": false,
  "eventTime": 1700000008000
}
```

## ContactRecordingResumeFailed
This is triggered when an attempt to resume contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned for the resume request. Example values: `UNSUPPORTED_OPERATION_FOR_MEDIATYPE`.                                                     |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `162` (unsupported operation for media type).                                             |

</details>

```json
{
  "type": "ContactRecordingResumeFailed",
  "eventType": "RoutingMessage",
  "interactionId": "f0f71e97-26b6-41f0-8b23-da9c49085858",
  "orgId": "a9cf8d67-59cd-4b69-a397-2221e5fb260c",
  "queueMgr": "queue-manager",
  "interaction": {...},
  "reason": "UNSUPPORTED_OPERATION_FOR_MEDIATYPE",
  "reasonCode": 162,
  "trackingId": "87ede599-f9d9-4ccc-890d-3e43c5c3442f",
  "eventTime": 1700000009000
}
```

## ContactRecordingStarted
This is triggered when contact recording is successfully started for an interaction.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "ContactRecordingStarted",
  "eventType": "RoutingMessage",
  "interactionId": "c3b7a9e2-4f1d-4a83-9c50-2e8d1f6b2041",
  "orgId": "a6d9c4b7-3e2f-4a81-9b50-1e7c5d8a2042",
  "queueMgr": "dummy_qm",
  "interaction": {...},
  "trackingId": "f7a2c9d1-6b3e-4a83-9c50-1e6d7b2a2050",
  "eventTime": 1768911903735
}
```

## ContactRecordingStartFailed
This is triggered when a request to start contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**    | **Description**                                                                                                    |
|--------------|--------------------------------------------------------------------------------------------------------------------|
| `reason`     | Failure reason returned on why the recording start request failed. Example values: `MEDIA_MANAGER_INTERNAL_ERROR`. |
| `reasonCode` | Numeric code associated with the failure reason. Example values: `100` (`MEDIA_MANAGER_INTERNAL_ERROR`).           |

</details>

```json
{
  "type": "ContactRecordingStartFailed",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "interaction": {...},
  "queueMgr": "queue-manager-1",
  "reason": "MEDIA_MANAGER_INTERNAL_ERROR",
  "reasonCode": 100,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## ContactRecordingStopFailed
This is triggered when a request to stop contact recording fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned on why the recording stop request failed. Example values: `MEDIA_MANAGER_INTERNAL_ERROR`.                                          |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `100` (`MEDIA_MANAGER_INTERNAL_ERROR`).                                                   |

</details>

```json
{
  "type": "ContactRecordingStopFailed",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "interaction": {...},
  "reason": "MEDIA_MANAGER_INTERNAL_ERROR",
  "queueMgr": "queue-manager-1",
  "reasonCode": 100,
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## ContactRecordingStopped
This is triggered when contact recording is successfully stopped for an interaction.

For field details, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

```json
{
  "type": "ContactRecordingStopped",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "eventTime": 1700000000000
}
```

## ParticipantPostCallActivity
This is triggered when post-call activity starts for a participant on the main or consult leg of an interaction, typically after the customer leaves while the interaction or consult leg remains active.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**         | **Description**                                                                                                                            |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `participantId`   | Identifier of the participant for whom post-call activity started.                                                                         |
| `participantType` | Type of participant for whom post-call activity started. Example values: `Agent`, `DN`.                                                    |
| `callLegType`     | Indicates whether the post-call activity applies to the main leg or consult leg. Example values: `MAIN_CALL`, `CONSULT`.                   |

</details>

```json
{
  "type": "ParticipantPostCallActivity",
  "eventType": "RoutingMessage",
  "interactionId": "interaction-id-1",
  "orgId": "org-id-1",
  "queueMgr": "queue-manager-1",
  "participantId": "participant-id-1",
  "interaction": {...},
  "trackingId": "tracking-id-1",
  "participantType": "Agent",
  "callLegType": {
    "type": "MAIN_CALL"
  },
  "eventTime": 1700000000000
}
```

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

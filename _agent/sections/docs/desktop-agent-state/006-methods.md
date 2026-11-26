---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent State Information Module
- Methods
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-agent-state). [Full Markdown](../../../../docs/desktop-agent-state.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Read agent information and manage availability by media channel with the Desktop SDK.

## Parent context

## Agent State Information Module

The `Desktop.agentStateInfo` module listens for the latest data updates of agent related information.

**Example**

```typescript
import { Service } from "@wxcc-desktop/sdk-types";

type IdleCodeData = { id: string; name: string };

type LatestInfoData = {
  agentName?: string,
  agentProfileID?: string,
  agentSessionId?: string,
  teamId?: string,
  teamName?: string,
  dn?: string,
  status?: string,
  /** @deprecated Global status; not valid with granular state control. Consume agent state from channelsStatesMap instead. */
  subStatus?: string,
  /** Per-channel agent state (agentState, stateChangeTimestamp, etc.). Keyed by channel type (e.g. telephony, chat). With granular state control, consume agent state from this instead of subStatus. */
  channelsStatesMap?: Record<string, { agentState?: string; stateChangeTimestamp?: number; pendingIdle?: boolean; auxCodeId?: string; availableChannelCount?: number | null; totalChannelCount?: number | null; stateChangeReason?: string; lastIdleCodeChangeTimestamp?: number | null; [key: string]: unknown }>,
  idleCodes?: Service.Aqm.Configs.Entity[],
  idleCode?: IdleCodeData,
  wrapupCodes?: Service.Aqm.Configs.Entity[],
  outDialRegex?: string,
  isOutboundEnabledForTenant?: boolean,
  isOutboundEnabledForAgent?: boolean,
  isAdhocDialingEnabled?: boolean,
  isAgentAvailableAfterOutdial?: boolean,
  isEndCallEnabled?: boolean,
  isEndConsultEnabled?: boolean,
  allowConsultToQueue?: boolean,
  isCampaignManagementEnabled?: boolean,
  agentPersonalStatsEnabled?: boolean
};
```

These fields may be unavailable until the module loads or when the corresponding feature is disabled. Guard optional fields before reading them. Nested idle-code fields apply when `idleCode` is present.

The following table lists the payload details:

| Name                         | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                               | Required |
| ---------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| agentName | String | Agent's name. | No |
| agentProfileID | String | Agent profile identifier. | No |
| agentSessionId | String | Agent session identifier. | No |
| teamId                       | String  | Unique identifier of the team.                                                                                                                                                                                                                                                                                                                                                                                            | No       |
| teamName                     | String  | Name of the team.                                                                                                                                                                                                                                                                                                                                                                                                         | No       |
| dn                           | String  | Dial number (DN) to the entry point.                                                                                                                                                                                                                                                                                                                                                                                      | No       |
| status                       | String  | Agent log in status such as LoggedIn.                                                                                                                                                                                                                                                                                                                                                                                     | No       |
| subStatus                    | String  | **Deprecated.** Global agent availability status (e.g. Available). Not valid with granular state control; consume agent state from **channelsStatesMap** instead.                                                                                                                                                                                          | No       |
| channelsStatesMap            | Object  | Map keyed by channel type (e.g. telephony, chat, email, social). Each value has agentState, stateChangeTimestamp, pendingIdle, auxCodeId, availableChannelCount, totalChannelCount, stateChangeReason, lastIdleCodeChangeTimestamp, and related fields. With granular state control, consume agent state from this map for status and state timestamps per channel.                                                                                                            | No       |
| idleCodes                    | Array   | Indicates the reason that the agent is idle and not available for any routed requests. The agent changes the state from Available to any configured idle codes. Example: Idle, Coffee break, Meeting, Tea.                                                                                                                                                                                                                | No       |
| idleCode                     | Object  | Indicates the current reason that the agent is idle. For example, the agent changed the idle state from Coffee break to Meeting.When the agent is in the Available state, the idleCode is undefined.                                                                                                                                                                                                                      | No       |
| --> id                       | String  | Idle code unique identifier.                                                                                                                                                                                                                                                                                                                                                                                              | Yes      |
| -->name                      | String  | Name of the reason code for the idle state, currently used by the agent. Example: Idle, Coffee break, Meeting, Tea.                                                                                                                                                                                                                                                                                                       | Yes      |
| wrapupCodes                  | Array   | The wrap up reason codes indicating that the agent has ended the interactions with the customer                                                                                                                                                                                                                                                                                                                           | No       |
| outDialRegex                 | String  | Outdial regular expression validity.                                                                                                                                                                                                                                                                                                                                                                                      | No       |
| isOutboundEnabledForTenant   | Boolean | Determines whether the outbound feature is enabled for the tenant.<br>- True—Enables the outbound feature for the tenant.<br>- False—Disables the outbound feature for the tenant.                                                                                                                                                                                                                                        | No       |
| isOutboundEnabledForAgent    | Boolean | Determines whether the outbound feature is enabled for the agent.<br>- True—Enables the outbound feature for the agent.<br>- False—Disables the outbound feature for the agent.                                                                                                                                                                                                                                           | No       |
| isAdhocDialingEnabled        | Boolean | Determines whether an agent can use a phone number that is not stated in the enterprise address book to make an outdial call.<br>- True—An agent is allowed to use phone numbers (using the **Dialpad**) that are not stated in the enterprise address book to make an outdial call.<br>- False—An agent is allowed to use only the phone numbers that are stated in the enterprise address book to make an outdial call. | No       |
| isAgentAvailableAfterOutdial | Boolean | Determines whether an agent is available or not after the outdial call ends.<br>- True—The agent is available after the outdial call ends, and the agent state is set as Available.<br>- False—The agent is not available after the outdial call ends, and the agent state is set as Idle.                                                                                                                                | No       |
| isEndCallEnabled             | Boolean | Determines whether an agent can end a voice call or not.<br>- True—Enables an agent to end a voice call.<br>- False—Disables an agent to end a voice call, and the agent must ask the customer to end the voice call.                                                                                                                                                                                                     | No       |
| isEndConsultEnabled          | Boolean | Determines whether an agent can end a consult call or not. The default value is true.<br>- True—Enables an agent to end a consult call.<br>- False—Disables an agent to end a consult call.                                                                                                                                                                                                                               | No       |
| allowConsultToQueue          | Boolean | Determines whether to consult an active call to a queue.<br>- True—Enables the consult call to a queue.<br>- False—Disables the consult call to a queue.                                                                                                                                                                                                                                                                  | No       |
| isCampaignManagementEnabled  | Boolean | Determines whether the outbound campaign call feature is enabled or not.<br>- True—Enables the outbound campaign call feature for an agent.<br>- False—Disables the outbound campaign call feature for an agent.                                                                                                                                                                                                          | No       |
| agentPersonalStatsEnabled    | Boolean | Determines whether the Agent Performance Statistics (APS) reports page is enabled or not.<br>- True—Enables the Agent Performance Statistics (APS) reports page for an agent.<br>- False—Disables the Agent Performance Statistics (APS) reports page for an agent.                                                                                                                                                       | No       |

## Selected section

### Methods

#### latestData

Fetches the latest user related information.
Access `latestData` inside the `updated` event hander (See [Events](https://developer.webex.com/docs/desktop-agent-state#events) section). This will make sure that `agentstateinfo` module is loaded before accessing the property.


**Example**

```typescript
const onUpdated = () => {
  const latestData: LatestInfoData = Desktop.agentStateInfo.latestData;
  console.log(latestData);
};
Desktop.agentStateInfo.addEventListener("updated", onUpdated);

// Call this function during widget teardown.
function cleanupAgentStateListener() {
  Desktop.agentStateInfo.removeEventListener("updated", onUpdated);
}
```

**Returns**
`{Object}` Lists the latest user related information.

**Example Response**

```json
{
    "agentName": "John Doe",
    "teamName": "Sales",
    "teamId": "964",
    "dn": "8895579172",
    "status": "LoggedIn",
    "subStatus": "Idle",
    "idleCodes": [{
        "id": "1646",
        "isDefault": false,
        "isSystem": true,
        "name": "Aux on Login"
    }],
    "wrapupCodes": [{
        "id": "2065",
        "isDefault": false,
        "isSystem": false,
        "name": "Wrapping up as customer disconnected"
    }],
    "outDialRegex": "([0-9a-zA-Z]+[-._])*[0-9a-zA-Z]+",
    "isOutboundEnabledForTenant": true,
    "isOutboundEnabledForAgent": true,
    "isAdhocDialingEnabled": true,
    "isAgentAvailableAfterOutdial": true,
    "isEndCallEnabled": true,
    "isEndConsultEnabled": true,
    "allowConsultToQueue": true,
    "isCampaignManagementEnabled": true,
    "agentPersonalStatsEnabled": true
}
```

#### stateChange(state, auxCodeIdArray)

**Deprecated:** Use [stateChangeV2()](https://developer.webex.com/docs/desktop-agent-state#statechangev2channeltype-state-auxcodeid-reason-agentid) for channel-specific state changes. The [Contact Center changelog](https://developer.webex.com/docs/api/changelog/webex-contact-center) announces deprecation beginning in March 2026.

Changes the state of an agent. For example from Available to Idle.

**Example**

```javascript
await Desktop.agentStateInfo.stateChange({
  state: "Available",
  auxCodeIdArray: "0"
});

// An example for Idle with an Idle Code

await Desktop.agentStateInfo.stateChange({
  state: "Meeting",
  auxCodeIdArray: "3bdbf3f3-0232-4ae3-b26c-16437c18a13d"
});
```

**Parameters**

| Name           | Type   | Description                           | Required |
| -------------- | ------ | ------------------------------------- | -------- |
| state          | String | Current agent state.                  | Yes      |
| auxCodeIdArray | String | Unique identifier of the agent state. | Yes      |

**Returns**

`{Object}` Lists the agent state change information.

**Example Response**

```json
{
    "data": {
        "agentId": "7c867aa9-ec768-341a-b767-e5hd6ae7g701",
        "agentSessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
        "auxCodeId": "0",
        "connectedChannels": [
            "38136791-cf79-4663-a5d0-39b0d094abf8"
        ],
        "eventType": "AgentDesktopMessage",
        "lastIdleCodeChangeTimestamp": null,
        "lastStateChangeReason": "",
        "lastStateChangeTimestamp": 1612245463183,
        "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
        "status": "LoggedIn",
        "subStatus": "Available",
        "trackingId": "9008a4a0-651b-11eb-a97d-0d76c582d799",
        "type": "AgentStateChangeSuccess"
    },
    "orgId": "f111e3af-1a45-42ef-9erf-4562354b8a25",
    "trackingId": "notifs_aa848b62-4fcf-4d4c-95ad-1233bb7f899c",
    "type": "AgentStateChange"
}
```
#### stateChangeV2(channelType, state, auxCodeId, reason, agentId)

Changes the state of a particular channel for the agent. For example from Available to Idle for "Chat" channel.
**Note**: For one channelType, all the channels must have same state. For example: 5 channels for type "Chat" will always have same state, while "Telephony" can have different state than "Chat".

**Example**

```javascript
await Desktop.agentStateInfo.stateChangeV2({
  channelType: ["telephony", "chat"],
  state: "Available",
  auxCodeId: "0",
  reason: "Available",
  agentId: "1a80ba23-194b-49af-9b93-074b3ecc852a",
});

// An example for Idle with an Idle Code

await Desktop.agentStateInfo.stateChangeV2({
  channelType: ["telephony"],
  state: "Idle",
  auxCodeId: "3bdbf3f3-0232-4ae3-b26c-16437c18a13d",
  reason: "Lunch",
  agentId: "1a80ba23-194b-49af-9b93-074b3ecc852a",
});
```

**Parameters**

| Name           | Type     | Description                                             | Required |
| -------------- | -------- | ------------------------------------------------------- | -------- |
| channelType    | String[] | Channel types for which the state needs to be applied.  | Yes      |
| state          | String   | Agent state to be applied.                              | Yes      |
| auxCodeId      | String   | Unique identifier of the agent state.                   | Yes      |
| reason         | String   | Reason for changing the state.                          | NO       |
| agentId        | String   | Unique identifier for the agent whose state is changed. | Yes      |

**Returns**

Multiple `{Object}` Lists the agent state change information per channel. The number of responses is equal to the number of channels mentioned in the channelType array.

**Timestamp units:** The `agentChannelStateDetail` fields in SDK response and event payloads use epoch milliseconds, as defined by the Contact Control API contract. This differs from the `STORE.agent.channelsStatesMap` fields documented in [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout#storeagent-agent-profile-attributes), which use epoch seconds. Use the units for the source you consume; a seconds value needs multiplication by 1,000 before passing it to `new Date()`.
NOTE: The responses are separate. NOT a single array of objects.

**Example Response**

```json
{
  "data": {
    "agentId": "1a80ba23-194b-49af-9b93-074b3ecc852a",
    "channelType": "telephony",
    "agentChannelStateDetail": {
      "agentState": "Available",
      "pendingIdle": false,
      "auxCodeId": "0",
      "availableChannelCount": 1,
      "manuallyAssignedChannelCount": null,
      "manuallyAssignedAvailableChannelCount": null,
      "totalManuallyAssignedChannelCount": null,
      "totalChannelCount": 1,
      "stateChangeTimestamp": 1757579405000,
      "stateChangeReason": "Available",
      "lastIdleCodeChangeTimestamp": 1757578805000
    },
    "changedBy": null,
    "changedById": null,
    "changedByName": null,
    "connectedChannels": ["38136791-cf79-4663-a5d0-39b0d094abf8"],
    "agentSessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
    "type": "AgentChannelStateChanged"
  },
  "orgId": "b33fb142-4d65-4781-9899-19b0363cd45f",
  "trackingId": "notifs_aa848b62-4fcf-4d4c-95ad-1233bb7f899c",
  "type": "AgentDesktopMessage"
}
```
```json
{
  "data": {
    "agentId": "1a80ba23-194b-49af-9b93-074b3ecc852a",
    "channelType": "chat",
    "agentChannelStateDetail": {
      "agentState": "Available",
      "pendingIdle": false,
      "auxCodeId": "0",
      "availableChannelCount": 1,
      "manuallyAssignedChannelCount": null,
      "manuallyAssignedAvailableChannelCount": null,
      "totalManuallyAssignedChannelCount": null,
      "totalChannelCount": 2,
      "stateChangeTimestamp": 1757579405000,
      "stateChangeReason": "Available",
      "lastIdleCodeChangeTimestamp": null
    },
    "changedBy": null,
    "changedById": null,
    "changedByName": null,
    "connectedChannels": ["38136791-cf79-4663-a5d0-39b0d094abf8", "4a235679-de68-5774-b651-nm76d094dj67"],
    "agentSessionId": "3d017488-527a-4e89-9313-5d4eb353c789",
    "type": "AgentChannelStateChanged"
  },
  "orgId": "b33fb142-4d65-4781-9899-19b0363cd45f",
  "trackingId": "notifs_aa848b62-4fcf-4d4c-95ad-1233bb7f899c",
  "type": "AgentDesktopMessage"
}
```

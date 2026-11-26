---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent State Information Module
- Events
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

### Events

#### addEventListener

Listens to an event named **updated** that is logged if the dn, status, or subStatus field is changed.

**Deprecation:** The **subStatus** field (global status) in the **updated** event is not valid with granular state control. Consume agent state from **STORE.agent.channelsStatesMap** and use the **eAgentChannelStateChanged** event for state changes and **stateChangeTimestamp** per channel.

For more information, see [addEventListener(event, handler)](https://developer.webex.com/docs/desktop-contact-events#addeventlistenerevent-handler).

**Example**

```javascript
Desktop.agentStateInfo.addEventListener("updated", updatedList => {
  console.log(updatedList);
});
```

**Example event payload**

```json
[
  {
    "name": "dn",
    "value": "+12580258011",
    "oldValue": ""
  },
  {
    "name": "status",
    "value": "LoggedIn",
    "oldValue": "DefaultState"
  },
  {
    "name": "subStatus",
    "value": "Available",
    "oldValue": ""
  }
]
```
**NOTE**: While using stateChangeV2 api, the listener needs to be changed from "updated" to "eAgentChannelStateChanged". This is a breaking change, and will NOT work with "updated".

**Example**

```javascript
Desktop.agentStateInfo.addEventListener("eAgentChannelStateChanged", eventData => console.log(eventData));

```

**Example event payload**

```javascript
const channelStateEvent = {
  agentId: "1a80ba23-194b-49af-9b93-074b3ecc852a",
  orgId: "b33fb142-4d65-4781-9899-19b0363cd45f",
  channelType: "telephony",
  agentChannelStateDetail: {
    agentState: "Available",
    pendingIdle: false,
    auxCodeId: "0",
    availableChannelCount: 1,
    manuallyAssignedChannelCount: null,
    manuallyAssignedAvailableChannelCount: null,
    totalManuallyAssignedChannelCount: null,
    totalChannelCount: 4,
    stateChangeTimestamp: 1757579405000,
    stateChangeReason: "Available",
    lastIdleCodeChangeTimestamp: 1757578805000
  },
  changedBy: null,
  changedById: null,
  changedByName: null,
  connectedChannels: ["38136791-cf79-4663-a5d0-39b0d094abf8"],
  agentSessionId: "3d017488-527a-4e89-9313-5d4eb353c789",
  trackingId: "9008a4a0-651b-11eb-a97d-0d76c582d799",
  type: "AgentChannelStateChanged",
  eventType: "AgentDesktopMessage"
}
```

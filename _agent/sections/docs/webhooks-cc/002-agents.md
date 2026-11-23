---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Agents
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks-cc). [Full Markdown](../../../../docs/webhooks-cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Contact Center webhook event types, resource versions, and event-specific payload fields.

---

<a id="using-webhooks"></a>

<a id="overview"></a>

## Selected section

## Agents

The agent resource encapsulates the entities which handle the tasks through interactions with customers. An agent can be either a human or bot, and can be either the entity directly handling the task, or an assisting entity i.e. a supervisor. Agents are summarized by the groups they belong to (organization and team), details for the tasks they handle, and their overall availability. For recovery queries, consult [Get Agent Activities](https://developer.webex.com/docs/api/v1/agents/get-agent-activities) for supported query windows.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `agent` | [`agent:login`](https://developer.webex.com/docs/webhooks-cc#agent-login) | An Agent has logged in. | `agent:1.0.0`, `agent:2.0.0` |
| `agent` | [`agent:logout`](https://developer.webex.com/docs/webhooks-cc#agent-logout) | An Agent has logged out. | `agent:1.0.0`, `agent:2.0.0` |
| `agent` | [`agent:state_change`](https://developer.webex.com/docs/webhooks-cc#agent-state-change) | An Agent’s state has changed. | `agent:1.0.0` |
| `agent` | [`agent:channel_state_change`](https://developer.webex.com/docs/webhooks-cc#agent-channel-state-change) | An agent's state changed at the channel level. | `agent:2.0.0` |
| `agent` | [`agent:channelType_state_change`](https://developer.webex.com/docs/webhooks-cc#agent-channeltype-state-change) | An agent's state changed for a specific channel type. | `agent:2.0.0` |

<a id="agent-login"></a>

### Agent Login

`agent:login`

**Resource Version: agent:1.0.0, agent:2.0.0**

An event indicating that an Agent has logged in.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who logged in. | `"8e18afd-db79-449b-b4f5-ae4f1d49f45e"` |
| `destination` | `string` | The phone number that is associated with the agent. | `"31476521"` |
| `profileType` | `string` | The multimedia profile type of the agent. Can be Blended, Blended Real-time, or Exclusive. | `"BLENDED"` |
| `idleCodeId` | `string` | The idle code of the agent when logged in. | `"5"` |
| `currentState` | `string` | The current state that the agent is in. | `"Idle"` |
| `createdTime` | `integer` | The time that the login event occurred in epoch milliseconds. | `160269666391` |
| `teamId` | `string` | The ID associated with an agent’s team. | `"3ce57020-dfd7-47fd-91a1-2783bf4a08e5"` |

<a id="agent-logout"></a>

### Agent Logout

`agent:logout`

**Resource Version: agent:1.0.0, agent:2.0.0**

An event indicating that an Agent has logged out.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who logged out. | `"8e18afd-db79-449b-b4f5-ee4f14d9f45e"` |
| `currentState` | `string` | The current state that the agent is in. | `"logged-out"` |
| `loggedOutBy` | `string` | The mechanism used to log the agent out. | `"SELF"` |
| `createdTime` | `integer` | The time that the logout event occurred in epoch milliseconds. | `160269666391` |

<a id="agent-state-change"></a>

### Agent State Change

`agent:state_change`

**Resource Version: agent:1.0.0**

An event indicating that an Agent’s state has changed.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who is handling the contact. | `"8e18afd-db79-449b-b4f5-ee4f14d9f45e"` |
| `currentState` | `string` | The current state of the agent. Can be idle, available, ringing, not-responding, connected, on-hold, hold-done, consulting, conferencing, consult-done, wrapup, wrapup-done. | `"idle"` |
| `destination` | `string` | The phone number that is associated with the agent. | `"9900163437"` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXlp8E3f-KJXJ6KOPIK"` |
| `taskId` | `string` | The ID associated with a specific interaction. | `"40fa44a7-b640-4b72-a8cd-5a0502ab2e81"` |
| `createdTime` | `integer` | The time that the state_change event occurred in epoch milliseconds. | `160269666391` |
| `idleCodeId` | `string` | The idle code of the agent when currentState is idle. | `"2651"` |
| `connectedChannels` | `string[]` | List of channels that agent is currently handling. | `["4fae000e-f460-4b5c-8b05-02f7fb5a8061", "4fae000e-fabb-4"]` |
| `wrapUpAuxCodeId` | `string` | The wrapup code the agent selects when ending a task. | `"3183"` |
| `teamId` | `string` | The ID associated with an agent’s team. | `"3ce57020-dfd7-47fd-91a1-2783bf4a08e5"` |

<a id="agent-channel-state-change"></a>

### Agent Channel State Change

`agent:channel_state_change`

**Resource Version: agent:2.0.0**

This event indicates that an agent's state has changed at the channel level. It is available under resource version agent:2.0.0.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent who is handling the contact. | `"8e18afd-db79-449b-b4f5-ee4f14d9f45e"` |
| `agentCiUserId` | `string` | The CI user ID associated with the agent. | `"68b1a6bd-1d3e-4cdb-9cb2-1ecd9faaf53d"` |
| `currentState` | `string` | The current state of the agent. Can be idle, available, ringing, not-responding, connected, on-hold, hold-done, consulting, conferencing, consult-done, conference-done, wrapup, wrapup-done. | `"idle"` |
| `channelId` | `string` | The ID of the channel associated with the agent. | `"bc7eedd6-42c6-45c5-9c94-2d34123317e6"` |
| `channelType` | `string` | The type of channel associated with the agent. | `"telephony"` |
| `destination` | `string` | The phone number that is associated with the agent. | `"9900163437"` |
| `queueId` | `string` | The ID associated with an agent queue. | `"AXlp8E3f-KJXJ6KOPIK"` |
| `taskId` | `string` | The ID associated with a specific interaction. | `"40fa44a7-b640-4b72-a8cd-5a0502ab2e81"` |
| `createdTime` | `integer` | The time that the state_change event occurred in epoch milliseconds. | `160269666391` |
| `idleCodeId` | `string` | The idle code of the agent when currentState is idle. | `"2651"` |
| `wrapUpAuxCodeId` | `string` | The wrapup code the agent selects when ending a task. | `"3183"` |
| `teamId` | `string` | The ID associated with an agent's team. | `"3ce57020-dfd7-47fd-91a1-2783bf4a08e5"` |

<a id="agent-channeltype-state-change"></a>

### Agent ChannelType State Change

`agent:channelType_state_change`

**Resource Version: agent:2.0.0**

An event indicating that an Agent's state has changed for a specific channel type. This event is fired when an agent's availability or engagement state transitions within a particular media channel (e.g., telephony, chat, email, or social).

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `agentId` | `string` | The ID associated with the agent whose channel type state has changed. | `"11bafc46-ae09-4ddf-bf0b-26d24e924f9f"` |
| `agentCiUserId` | `string` | The CI user ID associated with the agent. | `"68b1a6bd-1d3e-4cdb-9cb2-1ecd9faaf53d"` |
| `currentState` | `string` | The current state of the agent for the given channel type. Valid agent states are:<br />**Available** — The agent is available in this channel type and can accept a contact.<br />**Idle** — The agent is currently logged in but not available in this channel type and cannot take contacts. This would be shown on the desktop by the Aux code selected (e.g., lunch).<br />**Engaged** — The agent is actively working on one or more contacts in this channel type.<br />**EngagedOther** — The agent is engaged with a channel type that, due to "Exclusive" or "Blended Realtime" multimedia profile settings, prevents them from accepting a contact in this channel type. For example, if an agent with an Exclusive profile is engaged on an email, they would be "EngagedOther" in Voice, Chat, and Social. Similarly, with a Blended Realtime profile, if the agent is engaged on a Chat contact, they would be "EngagedOther" in the Voice channel type.<br />**WrapUp** — The agent is currently performing wrap-up work on a contact and will transition to Available at conclusion if not working on another contact in that channel type.<br />**Reserved** — The agent has been selected by routing and is in the process of being invited (inbound or outbound). This state is typically short-lived. For cases where a campaign agent is reserved with a reservation call, their state will be Reserved in the voice channel as opposed to Engaged.<br />**LoggedOut** — Although technically not a managed agent state, this indicates the agent is not logged into the system. | `"Available"` |
| `channelType` | `string` | The channel type of the agent for which the state change applies. Can be set to telephony, social, email, or chat. A separate agent:channelType_state_change event is sent per channel type. In the event that the agent is setting more than one channel type state at once, multiple state change events are sent — one per channel type. | `"social"` |
| `pendingIdleState` | `boolean` | Indicates whether the agent has a pending idle state. The value is determined by the following conditions: first, the agent's sub_status must be set to idle (the agent has indicated they want to go idle). If not, pendingIdleState is **false**. Next, the agent's state in the current channel must not yet be idle (e.g., the agent is still Engaged or in WrapUp). If the agent's state in the channel is already idle, pendingIdleState is **false**. Finally, if not all channels in the channelType are idle, then pendingIdleState is **true** — otherwise it is **false**. When **true**, the agent is currently working or wrapping up one or more contacts and will transition to Idle at the conclusion. No further contacts will be given to them in that channel type. On the desktop, the output will reflect the selected Aux code (e.g., "Pending Coffee-Break").<br />Note: In non-voice channels, it is possible to directly set the agent state to Idle although one or more channels are active in a media type. | `false` |
| `idleCodeName` | `string` | The name of the idle (auxiliary) code selected by the agent. This field is populated when the agent's current state is Idle, or when pendingIdleState is true (the agent has selected an idle code but has not yet transitioned). Examples include "Meeting", "Lunch", or "Break". | `"Meeting"` |
| `teamId` | `string` | The ID associated with an agent's team. | `"088ca4da-085c-4563-9b71-d430721f0354"` |
| `createdTime` | `integer` | The time that the channelType_state_change event occurred, in epoch milliseconds. | `1768319367741` |

For agent-specific recovery queries, use [Get Agent Activities](https://developer.webex.com/docs/api/v1/agents/get-agent-activities).

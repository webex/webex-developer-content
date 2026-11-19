---
type: Guide
title: Webex Contact Center Web SDK | Events
display_title: Events
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-events
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-events)

Events in the Webex Contact Center Web SDK are required for multi-session environments, to ensure that your application stays synchronized across browser tabs and reacts promptly to agent and task updates.

---

Refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) to initialize `webex`, register the agent, and set up your `webex.cc` listeners.

## Agent Events

| **Event** | **Description** | **Payload** |
|---|---|---|
| `agent:stationLoginSuccess` | Emitted after a successful station login. | `AgentStationLoginSuccess` object |
| `agent:stationLoginFailed` | Emitted if the station login attempt fails. | - |
| `agent:reloginSuccess` | Emitted after a successful re-login to the station. | `AgentStationLoginSuccess` object |
| `agent:logoutSuccess` | Emitted after the agent logs out successfully. | `AgentLogoutSuccess` object |
| `agent:logoutFailed` | Emitted if the agent logout attempt fails. | - |
| `agent:stateChangeSuccess` | Emitted when any agent state change notification is received. | `AgentStateChangeSuccess` object |
| `agent:stateChangeFailed` | Emitted when a state change request fails. | - |
| `agent:multiLogin` | Emitted when the agent logs in from another station or session. | - |
| `agent:dnRegistered` | Emitted when the agent DN is registered successfully. | - |

### AgentStationLoginSuccess
```ts
{
  agentId: string;
  agentSessionId: string;
  auxCodeId: string | null;
  chatCount: number;
  deviceId: string;
  deviceType: "BROWSER" | "EXTENSION" | "AGENT_DN";
  dn: string;
  emailCount: number;
  eventTime: number;
  interactionIds: string[];
  lastIdleCodeChangeTimestamp: number;
  lastStateChangeTimestamp: number;
  mmProfile: { chat: number; email: number; social: number; telephony: number; };
  notifsTrackingId: string;
  orgId: string;
  profileType: string;
  roles: string[];
  siteId: string;
  skillProfileId: string;
  skillProfileName: string;
  skills: string[];
  status: string;
  subStatus: string;
  teamId: string;
  trackingId: string;
  type: "AgentStationLoginSuccess";
  voiceCount: number;
}
```

### AgentLogoutSuccess
```ts
{
  data: {
    agentId: string;
    agentSessionId: string;
    eventTime: number;
    loggedOutBy: "SELF" | "SYSTEM";
    logoutReason: string;
    orgId: string;
    roles: string[];
    status: "LoggedOut";
    subStatus: string;
    trackingId: string;
    type: "AgentLogoutSuccess";
  };
  orgId: string;
  trackingId: string;
  type: "Logout";
}
```

### AgentStateChangeSuccess
```ts
{
  data: {
    agentId: string;
    agentSessionId: string;
    auxCodeId: string | null;
    changedBy: "SELF" | "SUPERVISOR";
    changedById: string;
    changedByName: string;
    connectedChannels: string[];
    eventTime: number;
    lastIdleCodeChangeTimestamp: number;
    lastStateChangeReason: string;
    lastStateChangeTimestamp: number;
    orgId: string;
    status: string;
    subStatus: string;
    trackingId: string;
    type: "AgentStateChangeSuccess";
  };
  orgId: string;
  trackingId: string;
}
```

## Task Events

### Task Payload

```js
// task.data
{
  agentId: `string`,                // agent's unique ID
  eventTime: `number`,              // timestamp in epoch ms
  interaction: {
    interactionId: `string`,        // interaction ID
    createdTimestamp: `number`,     // epoch ms when interaction started
    currentVTeam: `string`          // current virtual team (queue) ID
  },
  mediaType: `string`,              // "telephony" | "chat" | "email" | "social"
  contactDirection: { type:`string` }, // "INBOUND" | "OUTBOUND"
  state: `string`,                  // e.g., "connected", "consulted", "new"
  orgId: `string`                   // organization ID
}
```

| **Event** | **Description** | **Payload** |
|---|---|---|
| `task:hydrate` | Emitted when active tasks are restored during a session resume or page reload. | `Task object` |
| `task:incoming` | Emitted when a new task reservation arrives for the agent. | `Task object` |
| `task:offerContact` | Emitted when a direct contact offer is pushed to the agent. | `Task object` |
| `task:assigned` | Emitted when a task has been fully assigned to the agent. | `Task object` |
| `task:hold` | Emitted when the agent puts the task on hold. | `Task object` |
| `task:unhold` | Emitted when a held task is resumed. | `Task object` |
| `task:end` | Emitted when a task completes or is ended. | {`Task object`, wrapupRequired: `boolean`} (Indicates if we need to wrapup the task or now) |
| `task:wrapup` | Emitted when wrap-up is initiated on a task. | `Task object` |
| `task:wrappedup` | Emitted when wrap-up completes and the task is removed. | `Task object` |
| `task:recordingPaused` | Emitted when call recording is successfully paused. | `Task object` |
| `task:recordingPauseFailed` | Emitted when pausing call recording fails. | `Task object` |
| `task:recordingResumed` | Emitted when call recording is successfully resumed. | `Task object` |
| `task:recordingResumeFailed` | Emitted when resuming call recording fails. | `Task object` |
| `task:consultCreated` | Emitted when the agent initiates a consult on an existing task. | `Task object` |
| `task:offerConsult` | Emitted when another agent offers a consult request. | `Task object` |
| `task:consulting` | Emitted when a consult is active (on both sender and recipient sides). | `Task object` |
| `task:consultAccepted` | Emitted when an incoming consult offer is accepted. | `Task object` |
| `task:consultQueueCancelled` | Emitted when a queue-based consult is cancelled before it reaches a queue. | `Task object` |
| `task:consultQueueFailed` | Emitted when a queue-based consult fails. | `Task object` |
| `task:consultEnd` | Emitted when a consult ends on this task. | `Task object` |
| `task:rejected` | Emitted when the agent rejects a task (RONA). | reason: `string` (Reason for task rejection) |
| `task:media` | Emitted on arbitrary media changes within the task. | `Task object` |

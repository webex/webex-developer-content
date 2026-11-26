---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-events
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-events). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-events.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Events in the Webex Contact Center Web SDK are required for multi-session environments, to ensure that your application stays synchronized across browser tabs and reacts promptly to agent and task updates.

---

Refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) to initialize `webex`, register the agent, and set up your `webex.cc` listeners.

## Selected section

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

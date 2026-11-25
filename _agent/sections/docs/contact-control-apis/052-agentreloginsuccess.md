---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentReloginSuccess
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

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

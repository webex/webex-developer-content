---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentStationLoginSuccess
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

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

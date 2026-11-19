---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_agent
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Parent context

## Webhook Payload Schemas

This section provides detailed schema information for each telephony webhook resource.

## Selected section

### telephony_agent

Notification of call queue agent changes.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `join` | The agent has joined or left a queue |
| `state` | The agent's state has changed |
| `code` | The agent has entered wrap-up codes |

#### Event: join

Notification with the information on the call queue the agent is joining or leaving.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `join` for this event. |
| `joinInfo` | array | Array of queue join information objects. |

##### Join Info Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueId` | string | The queue ID. |
| `hasCxEssentials` | boolean | Denotes if the call queue has Customer Experience Essentials license. |
| `queueAutoAnswer` | boolean | Denotes if calls routed from a Customer Assist call queue to an available agent are answered automatically. |
| `allowLogoff` | boolean | Denotes if the agent is allowed to log on/off from the queue. |
| `status` | string | Join status: `joined`, `unjoined`, or `unassigned`. |
| `skillLevel` | integer | Skill level of the agent (for Skill-Based Routing queues). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agent",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "join",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "joinInfo": [
      {
        "queueId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
        "hasCxEssentials": true,
        "queueAutoAnswer": true,
        "allowLogoff": true,
        "status": "joined",
        "skillLevel": 12
      }
    ]
  }
}
```

#### Event: state

Notification when a call queue agent state changes.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `state` for this event. |
| `acdStateInfo` | object | Agent state information object (see <a href="https://developer.webex.com/docs/call-control#acd-state-info-object">ACD State Info Object</a>). |

<a id="acd-state-info-object"></a>

##### ACD State Info Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `state` | string | Current state: `signIn`, `available`, `unavailable`, `wrapUp`, or `signOut`. |
| `stateModifiedBy` | string | Entity that triggered the change: `agent`, `supervisor`, `admin`, or `policy`. |
| `supervisorId` | string | The supervisor that triggered the state change (if applicable). |
| `policyReason` | string | Policy reason: `unreachable`, `no-answer`, `busy`, `other`, or `wrap-up`. |
| `wrapUpDetails` | object | Additional details when entering wrap-up state (see <a href="https://developer.webex.com/docs/call-control#wrap-up-details">Wrap-Up Details</a>). |
| `stateTimestamp` | string | Timestamp of the last agent state change. |
| `signinTimestamp` | string | Timestamp of the agent sign-in. |
| `totalAvailableTime` | integer | Total available time since last sign-in. |
| `averageWrapUpTime` | object | Average wrap-up time per handled call. Contains `value` field. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agent",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "state",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "acdStateInfo": {
      "state": "unavailable",
      "stateModifiedBy": "policy",
      "supervisorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9iNTlhMWY5NS1kMzMwLTRmMDEtYWUyNy1jNGM3M2I0YmVhYjE=",
      "policyReason": "wrap-up",
      "wrapUpDetails": {
        "queueId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
        "queueName": "cx_essential_name",
        "queueNumber": "+15146977514",
        "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
        "wrapUpChangeId": "WrapUpChange_id_01",
        "maxWrapUpEndTime": "2024-09-10T01:19:22.903Z",
        "remoteParty": {
          "name": "Espace Commun",
          "number": "888",
          "id": "Y2lzY29zcGFyazovL3VzL1BMQUNFLzcxMTVjNjYyLTY2NmYtNDEwMS1iMjUzLTU4OGVkMTIzNTk0MA",
          "idType": "PLACE",
          "privacyEnabled": false,
          "callType": "location"
        }
      },
      "stateTimestamp": "2023-09-13T15:19:08.280Z",
      "signinTimestamp": "2023-09-13T12:10:21.432Z",
      "totalAvailableTime": 0,
      "averageWrapUpTime": {
        "value": 10
      }
    }
  }
}
```

#### Event: code

Notification when a call queue agent enters a wrap-up code.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `code` for this event. |
| `wrapUpCodes` | array | Array of wrap-up code strings to tag the call with. |
| `callId` | string | Identifier of the call to tag. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agent",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "code",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "wrapUpCodes": ["Promotion", "Customer Follow-up"],
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtODkxMjU0MTQ6MA"
  }
}
```

---

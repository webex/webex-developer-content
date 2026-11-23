---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queue
- 'Event: nightPolicyTreatmentCompleted'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Parent context

## Webhook Payload Schemas

This section provides detailed schema information for each telephony webhook resource.

### telephony_queue

Notification of call queue calls progression.

## Selected section

#### Event: nightPolicyTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Night policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="https://developer.webex.com/docs/call-control#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="https://developer.webex.com/docs/call-control#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="https://developer.webex.com/docs/call-control#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "nightPolicyTreatmentCompleted",
    "eventTimestamp": "2010-04-23T15:12:10.325Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtMjcxOjA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "callcenter",
    "queueNumber": "+15146987610",
    "remoteParty": {
      "name": "john3 south",
      "number": "+15146987603",
      "privacyEnabled": false,
      "callType": "location"
    },
    "reason": "EOF"
  }
}
```

---

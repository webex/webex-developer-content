---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queue
- 'Event: callUpdated'
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

#### Event: callUpdated

Notification when the remote party attributes are modified while the call is in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information with updated remote party details (see <a href="https://developer.webex.com/docs/call-control#common-queue-entry-object">Common Queue Entry Object</a>). |
| `reason` | string | Update reason (see <a href="https://developer.webex.com/docs/call-control#call-update-reason-enum">Call Update Reason Enum</a>). |

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
    "eventType": "callUpdated",
    "eventTimestamp": "2010-04-20T13:26:05.048Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTgzNjU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T13:26:05.048Z",
      "remoteParty": {
        "number": "+17003334",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "reason": "Call Transferred"
  }
}
```

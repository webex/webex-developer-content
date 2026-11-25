---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queue
- 'Event: callStranded'
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

#### Event: callStranded

Notification when a call is identified as stranded and removed from the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="https://developer.webex.com/docs/call-control#common-queue-entry-object">Common Queue Entry Object</a>). |
| `redirect` | object | Redirect details (see <a href="https://developer.webex.com/docs/call-control#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |
| `redirections` | array | Array of redirection information (see <a href="https://developer.webex.com/docs/call-control#redirection-information">Redirection Information</a>). |

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
    "eventType": "callStranded",
    "eventTimestamp": "2010-04-20T00:23:47.613Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQ1NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T00:23:36.743Z",
      "removeTime": "2010-04-20T00:23:47.613Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    }
  }
}
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queue
- 'Event: callPromoted'
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

#### Event: callPromoted

Notification when a call has been promoted to a different priority in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information with updated priority (see <a href="https://developer.webex.com/docs/call-control#common-queue-entry-object">Common Queue Entry Object</a>). |
| `position` | integer | The new position of the call in the queue. |

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
    "eventType": "callPromoted",
    "eventTimestamp": "2010-04-20T14:56:26.140Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTk2NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_2_Name",
      "queueNumber": "+15006001027",
      "addTime": "2010-04-20T14:55:55.321Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "position": 2
  }
}
```

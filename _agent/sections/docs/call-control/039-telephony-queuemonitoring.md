---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queueMonitoring
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

### telephony_queueMonitoring

Notification of call queue performance metrics.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `updated` | Queue monitoring status has been updated |

#### Queue Monitoring Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `actorType` | string | Always `CALL_QUEUE` for this resource. |
| `eventType` | string | Always `updated` for this payload. |
| `queueName` | string | The name of the call queue. |
| `monitoringStatus` | object | Queue monitoring status object. |

##### Queue Monitoring Status Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `averageHandlingTime` | object | Average handling time for calls to this queue. Contains `value` field. |
| `expectedWaitTime` | object | Expected wait time for calls. Not present if no agents in Available or Wrap-Up state. Contains `value` field. |
| `averageSpeedOfAnswer` | object | Average speed of answer for calls. Contains `value` field. |
| `longestWaitTime` | object | Longest wait time of any calls in the queue. Contains `value` field. |
| `numCallsInQueue` | object | Number of calls in the queue. Contains `value` field. |
| `numAgentsAssigned` | integer | Number of agents assigned to the queue. |
| `numAgentsStaffed` | integer | Number of agents staffing the queue. |
| `numStaffedAgentsIdle` | integer | Number of staffed agents that are idle (not on a call and in available state). |
| `numStaffedAgentsUnavailable` | integer | Number of staffed agents in the unavailable state. |

#### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svOTg3NjU0MzItYWJjZC0xMjM0LWVmZ2gtMTIzNDU2Nzg5MGFi",
  "name": "My Queue Monitoring Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queueMonitoring",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "ownedBy": "org",
  "status": "active",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjMTIzZGVmNDU2",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "updated",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "queueName": "Support Queue",
    "monitoringStatus": {
      "averageHandlingTime": {
        "value": 180
      },
      "expectedWaitTime": {
        "value": 45
      },
      "averageSpeedOfAnswer": {
        "value": 30
      },
      "longestWaitTime": {
        "value": 120
      },
      "numCallsInQueue": {
        "value": 5
      },
      "numAgentsAssigned": 10,
      "numAgentsStaffed": 8,
      "numStaffedAgentsIdle": 3,
      "numStaffedAgentsUnavailable": 2
    }
  }
}
```

---

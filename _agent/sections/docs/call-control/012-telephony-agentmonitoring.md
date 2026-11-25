---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_agentMonitoring
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

### telephony_agentMonitoring

Notification of call queue agent performance metrics.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `updated` | Agent monitoring status has been updated |

#### Agent Monitoring Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `updated` for this payload. |
| `monitoringStatus` | object | Agent monitoring status object (see <a href="https://developer.webex.com/docs/call-control#agent-monitoring-status-object">Agent Monitoring Status Object</a>). |

<a id="agent-monitoring-status-object"></a>

##### Agent Monitoring Status Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `averageACDCallTime` | object | Average call time for call queue calls since last sign-in. Contains `value` field. |
| `averageACDOutgoingCallTime` | object | Average call time for outgoing call queue calls since last sign-in. Contains `value` field. |

#### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agentMonitoring",
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
    "eventType": "updated",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "monitoringStatus": {
      "averageACDCallTime": {
        "value": 6154
      },
      "averageACDOutgoingCallTime": {
        "value": 0
      }
    }
  }
}
```

---

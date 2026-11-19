---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_calls
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

### telephony_calls

Notification of calls progression through each state.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `originating` | An outgoing call is being originated |
| `originated` | An outgoing call has been originated |
| `received` | An incoming call was received |
| `answered` | The call was answered |
| `held` | The call was placed on hold |
| `resumed` | The call was resumed from hold |
| `recordingStarting` | Call recording is starting |
| `recordingStarted` | Call recording has started |
| `recordingPaused` | Call recording was paused |
| `recordingResumed` | Call recording was resumed |
| `recordingStopped` | Call recording was stopped |
| `disconnected` | The call was disconnected |
| `transferred` | The call was transferred |
| `bargedIn` | The call was barged into |
| `retrieved` | The call was retrieved |
| `pickedUp` | The call was picked up |
| `forwarded` | The call was forwarded |
| `updated` | The call was updated |

#### Call Data Fields

| **Field** | **Type** | **Required** | **Description** |
|-----------|----------|--------------|-----------------|
| `callId` | string | Yes | The call identifier of the call. |
| `callSessionId` | string | Yes | The call session identifier. Can be used to correlate multiple calls in the same session. |
| `personality` | string | Yes | The personality of the call: `originator`, `terminator`, or `clickToDial`. |
| `state` | string | Yes | Current state: `connecting`, `alerting`, `connected`, `held`, `remoteHeld`, or `disconnected`. |
| `remoteParty` | object | Yes | The remote party's details (see <a href="https://developer.webex.com/docs/call-control#party-information">Party Information</a>). |
| `created` | string | Yes | The date and time the call was created. |
| `muteCapable` | boolean | Yes | Indicates whether the call supports mute/unmute APIs. |
| `muted` | boolean | Yes | Indicates whether the call is currently muted. |
| `appearance` | integer | No | The appearance value for the call (for ordering on devices). |
| `answered` | string | No | The date and time the call was answered. |
| `disconnected` | string | No | The date and time the call was disconnected. |
| `redirections` | array | No | List of previous redirections (see <a href="https://developer.webex.com/docs/call-control#redirection-information">Redirection Information</a>). |
| `recall` | object | No | Recall details for incoming calls (e.g., park recall). |
| `recordingState` | string | No | Recording state: `pending`, `started`, `paused`, `stopped`, or `failed`. |
| `completedElsewhere` | boolean | No | Indicates if the call was completed elsewhere. |
| `parkedAgainstParty` | object | No | Details of the party against which this call is parked (see <a href="https://developer.webex.com/docs/call-control#party-information">Party Information</a>). |
| `executiveId` | string | No | The ID of the Executive for Executive Assistant service. |
| `allowedRecordingControls` | array | No | Recording controls allowed: `record`, `pause`, `stop`, `resume`. |
| `endpointId` | string | No | The ID of the endpoint linked to the call. |
| `endpointType` | string | No | Endpoint type: `CALLING_DEVICE`, `APPLICATION`, or `HOTDESKING_GUEST`. |
| `networkEndpointNumber` | string | No | The address of the network endpoint linked to the call. |
| `networkEndpointType` | string | No | Network endpoint type: `EXECUTIVE_ASSISTANT` or `SINGLE_NUMBER_REACH`. |

#### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_calls",
  "event": "created",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "creator",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "received",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtODkxMjU0MTQ6MA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "personality": "terminator",
    "state": "alerting",
    "muteCapable": false,
    "muted": false,
    "remoteParty": {
      "name": "Espace Commun",
      "number": "888",
      "placeId": "Y2lzY29zcGFyazovL3VzL1BMQUNFLzcxMTVjNjYyLTY2NmYtNDEwMS1iMjUzLTU4OGVkMTIzNTk0MA",
      "id": "Y2lzY29zcGFyazovL3VzL1BMQUNFLzcxMTVjNjYyLTY2NmYtNDEwMS1iMjUzLTU4OGVkMTIzNTk0MA",
      "idType": "PLACE",
      "privacyEnabled": false,
      "callType": "location"
    },
    "appearance": 1,
    "created": "2026-01-07T22:11:00.018Z",
    "completedElsewhere": false,
    "endpointId": "Y2lzY29zcGFyazovL3VzL0NBTExJTkdfREVWSUNFLzJjMzEyNGM4LWM1OWEtNDgwMC1iYmI1LTU5NDM4ZjUwMGZhNA",
    "endpointType": "CALLING_DEVICE"
  }
}
```

---

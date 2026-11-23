---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Object
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Call Object

After the lines have been registered, you can utilize call functionality on any of these registered lines. To initiate a call, you can use the `makeCall()` method when invoked on a specific line. When an inbound call is received by the client from Webex Calling, the Calling SDK dispatches an event, and within the event payload, a call instance is returned.

This call instance, provided by the Calling SDK, is of type `ICall`. It provides a range of methods that enable you to perform specific actions and manage the call as it progresses through various states.

### Call Methods

| **Method** | **Description** | **Returns** | **Visibility** |
| --- | --- | --- | --- |
| `answer` | Accepts or answers an incoming call from Webex Calling. | `void` | Public |
| `dial` | Dials the outgoing call to the destination. | `void` | Public |
| `end` | Ends an ongoing call. | `void` | Public |
| `sendDigit` | Sends a DTMF digit on an established call. | `void` | Public |
| `mute` | Mutes the local stream of this call instance. | `void` | Public |
| `doHoldResume` | Places the remote end of this call on either hold/resume on the current state of the call. | `void` | Public |
| `completeTransfer` | Initiates a transfer towards a target. | `void` | Public |
| `updateMedia` | Updates the microphone stream used during the call. | `void` | Public |

### Call Events

| **Event** | **Description** | **Payload** |
| --- | --- | --- |
| `incoming_call` | Incoming call is received. | Call Object (`ICall`) |
| `caller_id` | Remote end calling information determined. | `CallId` |
| `progress` | Remote end is ringing or has provided a cut-through. | `CorrelationId(string)` |
| `connect` | The remote end has answered the call. | `CorrelationId(string)` |
| `established` | Two-way media has now been established. | `CorrelationId(string)` |
| `remote_media` | Remote media track received. Use this to play out remote media on client. | Track object (`MediaStreamTrack`) |
| `disconnect` | Remote end has disconnected the call. | `CorrelationId(string)` |
| `held` | Remote end has been put on hold successfully. | `CorrelationId(string)` |
| `resumed` | Remote end has been put on hold successfully. | `CorrelationId(string)` |
| `call_error` | An error has occurred in the call | Error object. `(CallError)` |
| `hold_error` | An error has occurred while placing call on hold. | Error object (`CallError`) |
| `resume_error` | An error has occurred while placing call on resume. | Error object (`CallError`) |
| `transfer_error` | An error has occurred while transferring the call. | Error object (`CallError`) |

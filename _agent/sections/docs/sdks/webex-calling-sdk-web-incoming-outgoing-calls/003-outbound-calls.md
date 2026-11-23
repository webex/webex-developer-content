---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Outbound Calls
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Outbound Calls

Create the `call` instance first for outbound calls using the `makeCall()` method of the `line` object.

```javascript
call = line.makeCall();
```

Trigger the `call` object's `dial()` method to initiate the call. This method requires a `localAudioStream` as an argument.

```javascript
call.dial({ localAudioStream });
```

Listen for events on the `call` object to track the further progress of the call and establish 2-way audio.

```javascript
call.on('progress', (correlationId: string) => {
  // Process call progress, this event indicates that the call is ringing on the called party side
});
```

```javascript
call.on('connect', (correlationId: string) => {
  // Process connect event, this is received when the call has been answered from the called party side
});
```

```javascript
call.on('remote_media', (track: MediaStreamTrack) => {
  // Add code to store remote audio received and use it to open media channel 2-way
});
```

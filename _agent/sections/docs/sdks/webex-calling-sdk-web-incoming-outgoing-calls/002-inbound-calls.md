---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Inbound Calls
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Inbound Calls

In order to receive incoming calls, listen for the `incoming_call` event on the `line` object.

```javascript
line.on('line:incoming_call', (call: ICall) => {
  //  Call object received. Store this object and listen for events on the call
});
```

Once the call is received by the application, you can use the `answer()` method to answer the call. This method requires a `localAudioStream` as an argument.

```javascript
call.answer({ localAudioStream });
```

Once the call is answered from the application side, listen for additional events received on the `call` instance such as `remote_media`, `disconnect`, `caller_id` `update`, etc. More details on those events can be found in the Call Events table above.


```javascript
call.on('remote_media', (track: MediaStreamTrack) => {
  // store remote audio received and use it to open media channel 2-way
});
```

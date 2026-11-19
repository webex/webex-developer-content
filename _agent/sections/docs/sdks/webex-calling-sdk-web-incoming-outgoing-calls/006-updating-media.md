---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Updating Media
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Updating Media

While a call is in progress, it's possible to update media to allow a developer to switch from one device to another. In order to do that, the `call` object provides an `updateMedia()` method.

First, create a `constraints` object using the new device ID and then pass that `constraints` object to the `Calling` object's `createMicrophoneStream()` method, creating a new `Stream` object.

### CDN

```javascript
const constraints = {
  audio: true,
  deviceId: 'DEVICE_ID'
};

const newStream = await Calling.createMicrophoneStream(constraints);
```

### NPM

```javascript
import {LocalMicrophoneStream} from '@webex/calling';

const constraints = {
  audio: true,
  deviceId: 'DEVICE_ID'
};

const localStream = navigator.mediaDevices.getUserMedia(constraints);
const audioTrack = localStream.getAudioTracks()[0];
const newStream = new LocalMicrophoneStream(new MediaStream([audioTrack])); 
```

Then, pass the `Stream` object to the `call` object's `updateMedia()` method.

```javascript
call.updateMedia(newStream);
```

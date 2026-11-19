---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Re-enable Browser Audio
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

When connected to a meeting, the following dialing capabilities are available:

- **Dial out**: Allows the system to call a user's phone, enabling it to be used as the audio input/output device for the meeting.
- **Dial in**: Permits users to call into Webex and use their phone as the meeting's audio input/output device.

<br/>

The SDK also provides functionality to remotely end phone calls in both of the above scenarios.

## Selected section

## Re-enable Browser Audio

If, after disconnecting the phone audio for a meeting, you want to enable computer audio (assuming it was not already enabled or was disconnected during the use of phone audio), depending on the SDK version:

### SDK 3.x

For 3.x SDKs to enable sending and receiving audio via the browser, send the flag `audioEnabled: true` in the `Meeting` object's [updateMedia](https://webex.github.io/webex-js-sdk/api/#meetingupdatemedia) method:

```js
await meeting.updateMedia({
  audioEnabled: true
});
```

### SDK 2.x

For the 2.x SDK to enable sending and receiving audio via the browser, send the flags `sendAudio: true` and `receiveAudio: true` as well as the `Stream` object to the `Meeting` object's [updateAudio](https://webex.github.io/webex-js-sdk/api/#meetingupdateaudio) method:

```js
await meeting.updateAudio({
  sendAudio: true,
  receiveAudio: true,
  stream
});
```

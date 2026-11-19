---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Create Streams
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-web-streams-and-effects.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex Meetings Web SDK version 3.0 introduces new APIs designed to facilitate the management of local media streams for audio, video, and screen sharing. This article explains how the `Streams` object functions with two newly added effects: `VirtualBackgroundEffect` and `NoiseReductionEffect`. Those effects and their corresponding methods are available in the plugin-meetings package.

---



> **Info**
>
> See the [kitchen sink app](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings) for examples of the effects.

## Selected section

## Create Streams

To create a stream, camera, microphone, or display, invoke the respective method while passing any required parameters:

```js
const cameraStream = await createCameraStream(cameraConstraints);

const microphoneStream = await createMicrophoneStream(audioConstraints);

const [localShareVideoStream, localShareAudioStream] = await createDisplayStreamWithAudio();
```

Here are the supported constraints:

```js
const cameraConstraints = {
    deviceId?: ConstrainDOMString;
    width?: ConstrainULong;
    height?: ConstrainULong;
    aspectRatio?: ConstrainDouble;
    frameRate?: ConstrainDouble;
    facingMode?: ConstrainDOMString;
};

const audioConstraints = {
    deviceId?: string;
    autoGainControl?: boolean;
    echoCancellation?: boolean;
    noiseSuppression?: boolean;
};
```

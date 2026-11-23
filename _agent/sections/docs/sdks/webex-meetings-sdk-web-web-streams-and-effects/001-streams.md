---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Streams
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

## Streams

The following new `Streams` classes have been introduced:

1. [LocalCameraStream](https://github.com/webex/webrtc-core/blob/main/src/media/local-camera-stream.ts)
2. [LocalMicrophone](https://github.com/webex/webrtc-core/blob/main/src/media/local-microphone-stream.ts)
3. [LocalDisplayStream](https://github.com/webex/webrtc-core/blob/main/src/media/local-display-stream.ts)
4. [LocalSystemAudioStream](https://github.com/webex/webrtc-core/blob/main/src/media/local-system-audio-stream.ts)


Import the `Streams` classes into your applications using the `plugin-meetings` package:

```js
import {
  LocalCameraStream,
  LocalMicrophoneStream,
  LocalDisplayStream,
  LocalSystemAudioStream,
  createCameraStream,
  createMicrophoneStream,
  createDisplayStream,
  createDisplayStreamWithAudio
} from '@webex/plugin-meetings';
```

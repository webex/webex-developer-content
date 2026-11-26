---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Apply the Noise Reduction Effect
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

## Apply the Noise Reduction Effect

To apply the noise reduction effect to a microphone stream:

```js
const microphoneStream = await createMicrophoneStream();

const effect = await webex.meetings.createNoiseReductionEffect();

meetingStreamsLocalAudio.srcObject = microphoneStream.outputStream;

const effect = await microphoneStream.addEffect(effect);

await effect.enable();
```

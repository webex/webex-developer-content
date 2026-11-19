---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Apply a Virtual Background Effect
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

## Apply a Virtual Background Effect

To apply a virtual background effect to your camera `Stream`:

1. Create a local camera stream with any desired constraints:

   ```js
   const cameraConstraints = { width: 640, height: 480 };

   const cameraStream = await createCameraStream(cameraConstraints);
   ```

2. Add the camera stream to the video `srcObject`:

   ```js
   meetingStreamsLocalVideo.srcObject = cameraStream.outputStream;
   ```

3. Create the virtual background effect using the `createVirtualBackgroundEffect()` method:

   ```js
   const effect = await webex.meetings.createVirtualBackgroundEffect();
   ```
  
   Since no parameters are specified, the `BLUR` background effect is created.

4. After creating the background effect, use the `cameraStream` object's `addEffect()` method to apply the effect to the camera stream:

   ```js
   const effect = await cameraStream.addEffect(effect);
   ```

5. Enable the effect to observe it in action on the video:

   ```js
   await effect.enable();
   ```

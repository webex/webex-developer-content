---
type: Guide
title: Web Calling SDK | Background Noise Reduction
display_title: Background Noise Reduction
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction)

This article explains how to enable Background Noise Reduction (BNR) for calls using the Webex Web Calling SDK.

## Prerequisites

To set up BNR for your Webex calls using the Web SDK:

1. The `webex` version should be `3.0.0` or higher.
2. The `@webex/calling` should be `3.0.1` or higher.
3. A valid Webex access token is required.

## Create LocalAudioStream

To add the `Background Noise Reduction (BNR)` effect to Webex calls, create a `LocalAudioStream` with the code below and the specified constraints:

```js
const constraints = {audio: true}

const localAudioStream = await Calling.createMicrophoneStream(constraints);
```

Include the SDK via a CDN or import it as shown:

```js
import Calling from 'webex';
```

For more details on importing `Calling`, see [Quickstart Guide](../quickstart-guide.md).

### Parameters



|**Parameter Name**| **Type**                | **Description**                                                      |**Mandatory**|
|------------------|-------------------------|----------------------------------------------------------------------|-------------|
| `constraints`    | `MediaTrackConstraints` |  The `MediaTrackConstraints` dictionary specifies a collection of media track capabilities, along with their respective permissible values or range of values. Please read about each of the supported `MediaTrackConstraints` [here](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#instance_properties). | No            |

## Creating & Adding Noise Reduction Effect

With `localAudioStream` established, create a noise reduction effect with the specified options and attach it to the stream:

```js
const effect = await Calling.createNoiseReductionEffect(options);
```

### Options



|**Parameter Name**| **Type** | **Description**                             |**Mandatory**|
|------------------|----------|---------------------------------------------|-------------|
| `authToken`      | `String` | The access token used for communication with Webex. | Yes  |
| `audioContext`   | `AudioContext` | An optional `AudioContext` to supply an existing `AudioContext`, otherwise a new one will be created. | No |
| `mode`           | `NoiseReductionMode` | Determines whether to run in `WORKLET` mode or `LEGACY` mode for older browsers. Defaults to `WORKLET`. | No |
| `workletProcessorURL`   | `String` | A URL to fetch the `AudioWorkletProcessor` to attach to the `AudioWorkletNode`. This is used to keep the audio computations from impacting UI performance. | No |
| `legacyProcessorURL`   | `String` | A URL to fetch the legacy processor that attaches to the deprecated `ScriptProcessorNode`. | No |

For more details on options listed above, see https://github.com/webex/web-media-effects?tab=readme-ov-file#noise-reduction 

After creating the effect, add it to the `LocalAudioStream`:

**Before webex `3.0.0-next.4` or @webex/calling `3.0.1-next.2`**

```js
await localAudioStream.addEffect('background-noise-removal', effect); 
```

**After webex `3.0.0-next.4` or @webex/calling `3.0.1-next.2`**

```js
await localAudioStream.addEffect(effect); 
```

### Parameters



|**Parameter Name**| **Type**               | **Description**                                  | **Mandatory** |
|------------------|------------------------|--------------------------------------------------|---------------|
| `effect`         | `NoiseReductionEffect` | An instance of the `NoiseReductionEffect` class. | Yes           |



> **Info**
>
> The Webex Web Calling SDK supports only the '**Noise Reduction**' effect.



## Enabling Background Noise Reduction

BNR effect has been added to the `LocalAudioStream` so you can enable it as shown below:


```js
let bnrEffect = await localAudioStream.getEffectByKind('noise-reduction-effect');

if (bnrEffect) {
    await bnrEffect.enable();
}
```

## Disabling Background Noise Reduction

To disable the BNR effect:

```js
let bnrEffect = await localAudioStream.getEffectByKind('noise-reduction-effect');

if (bnrEffect) {
    await bnrEffect.disable();
}
```

## Remove the BNR Effect

Dispose of the effect when it's no longer needed or during stream cleanup to prevent memory leaks. This is crucial when switching streams mid-call or when the microphone changes during a call.

To remove BNR:

```js
await localAudioStream.disposeEffects()
```

This action clears all the effects from the `LocalAudioStream` simultaneously.

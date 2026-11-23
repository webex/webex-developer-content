---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating & Adding Noise Reduction Effect
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-background-noise-reduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how to enable Background Noise Reduction (BNR) for calls using the Webex Web Calling SDK.

## Selected section

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

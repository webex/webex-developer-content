---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Create LocalAudioStream
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-background-noise-reduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how to enable Background Noise Reduction (BNR) for calls using the Webex Web Calling SDK.

## Selected section

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

For more details on importing `Calling`, see [Quickstart Guide](../../../../../docs/quickstart-guide.md).

### Parameters



|**Parameter Name**| **Type**                | **Description**                                                      |**Mandatory**|
|------------------|-------------------------|----------------------------------------------------------------------|-------------|
| `constraints`    | `MediaTrackConstraints` |  The `MediaTrackConstraints` dictionary specifies a collection of media track capabilities, along with their respective permissible values or range of values. Please read about each of the supported `MediaTrackConstraints` [here](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#instance_properties). | No            |

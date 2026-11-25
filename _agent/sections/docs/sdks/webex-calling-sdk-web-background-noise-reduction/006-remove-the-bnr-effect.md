---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Remove the BNR Effect
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-background-noise-reduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how to enable Background Noise Reduction (BNR) for calls using the Webex Web Calling SDK.

## Selected section

## Remove the BNR Effect

Dispose of the effect when it's no longer needed or during stream cleanup to prevent memory leaks. This is crucial when switching streams mid-call or when the microphone changes during a call.

To remove BNR:

```js
await localAudioStream.disposeEffects()
```

This action clears all the effects from the `LocalAudioStream` simultaneously.

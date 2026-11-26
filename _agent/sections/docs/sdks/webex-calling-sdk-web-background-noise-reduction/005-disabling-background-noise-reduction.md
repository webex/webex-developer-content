---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Disabling Background Noise Reduction
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-background-noise-reduction). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-background-noise-reduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how to enable Background Noise Reduction (BNR) for calls using the Webex Web Calling SDK.

## Selected section

## Disabling Background Noise Reduction

To disable the BNR effect:

```js
let bnrEffect = await localAudioStream.getEffectByKind('noise-reduction-effect');

if (bnrEffect) {
    await bnrEffect.disable();
}
```

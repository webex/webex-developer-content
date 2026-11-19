---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Effect Helper Methods
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

## Effect Helper Methods

Both effects offer the following helper methods:

- `effect.disable()` - Disables the effect.
- `effect.dispose()` - Removes the effect.
- `effect.setEnabled(true|false)` - Single method to enable or disable the effect. Pass `true` to enable the effect and `false` to disable.
- `stream.getEffectByKind(effectName)` - Return the effect added on the stream (either `noise-reduction-effect` or `virtual-background-effect`).
- `stream.getEffects()` - Retrieve all effects added to the stream.
- `stream.disposeEffects()` - Remove all effects from the stream.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-closed-captions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- CaptionItem Details
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-closed-captions). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-closed-captions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Closed captions offer a text alternative to spoken dialogue, enabling participants in a meeting to read spoken content. This becomes particularly useful in ensuring accessibility and understanding of the content being discussed during a meeting.

---

Each participant in the meeting can independently enable closed captions in the language they want to see the spoken content. In effect, all participants can enable captions in different languages at the same time enabling them to read spoken content in their own native language within same meeting.



> **Info**
>
> Available starting from SDK version 3.10.0.

## Selected section

## CaptionItem Details

The `CaptionItem` object holds the caption text, speaker ID, display name, and an `isFinal` flag. The `onCaptionArrived()` method triggers initially with each spoken word (`isFinal=false`). When the speaker pauses or stops, it refines the text for accuracy and context, triggering again with `isFinal=true`. The `isFinal=true` flag indicates that the sentence is complete.

For example the following spoken phrase, "Hello developer, how are you?" can trigger the following callbacks:

1. Callback 1: "hello" -> `isFinal=false`
2. Callback 2: "hello developer" -> `isFinal=false`
3. Callback 3: "hello developer how are" -> `isFinal=false`
4. Callback 4: "hello developer how are you and" -> `isFinal=false` (The word "and" was a false detection.)
5. Callback 5: "hello developer, how are you?" -> `isFinal=true` (If the speaker pauses or stops talking. Normalized statement in terms of context and grammar.)

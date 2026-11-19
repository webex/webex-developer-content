---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Mute or Unmute a Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-basic-webex-calling-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the fundamental steps for integrating call functionality using the Webex Android SDK.

## Selected section

## Mute or Unmute a Call

To mute a call:

```kotlin
call?.setSendingAudio(false)
```

To unmute a call:

```kotlin
call?.setSendingAudio(true)
```

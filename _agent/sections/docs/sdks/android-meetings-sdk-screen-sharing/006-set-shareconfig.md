---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Set ShareConfig
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your Android mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own Android application.

## Selected section

## Set ShareConfig

To set the share configuration, use one of the following options:

```kotlin
    // Default setting: no special optimization, max 3 FPS.    
    var shareConfig = ShareConfig(Call.ShareOptimizeType.Default, false)

    // Auto-detects sharing type, max 5 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.AutoDetection, false)

    // Optimizes screen sharing for video/motion, max 30 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.OptimizeVideo, false)

    // Optimizes video/motion sharing, max 30 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.OptimizeVideo, true)

    // Optimizes text/image sharing, max 5 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.OptimizeText, false)
```

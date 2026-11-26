---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- ShareMaxCaptureFPS
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your Android mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own Android application.

## Selected section

## ShareMaxCaptureFPS

The `ShareMaxCaptureFPS` method in `AdvancedSetting.kt` allows for setting the maximum fps during screen sharing. However, the Screenshare Optimization settings will override the `ShareMaxCaptureFPS` setting.

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.ShareMaxCaptureFPS(fps) as AdvancedSetting<*>)
```

Here are some scenarios showing the interaction between `ShareMaxCaptureFPS` and screenshare optimization from version 3.9.0:

* Set `ShareMaxCaptureFPS` to 10 and `OptimizeText` in `ShareConfig` to limit the FPS to 5.
* Set `ShareMaxCaptureFPS` to 3 and `OptimizeText` in `ShareConfig` to limit the FPS to 5.
* Set `ShareMaxCaptureFPS` to 10 and `OptimizeVideo` in `ShareConfig` to achieve a maximum FPS of 30.
* Set `ShareMaxCaptureFPS` to 7 without using `shareConfig` to achieve a maximum FPS of 7.
* Set `ShareMaxCaptureFPS` to 30 without using `shareConfig` to achieve a maximum FPS of 30.
* Do not set `ShareMaxCaptureFPS` or set it to 0 without using `shareConfig` to limit the FPS to 5.

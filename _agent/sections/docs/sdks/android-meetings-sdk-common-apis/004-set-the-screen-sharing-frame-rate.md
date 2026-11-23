---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-common-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Set the Screen Sharing Frame Rate
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-common-apis). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-common-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides an overview of the common APIs used to implement Webex functionality in your Android application.

---

It covers essential configurations such as setting video frame rates, toggling camera usage, enabling background video streaming, setting screen sharing frame rates, and configuring noise reduction. These APIs help you optimize the performance and quality of your Webex integration.

## Selected section

## Set the Screen Sharing Frame Rate

Set the maximum capture frame rate for screen sharing:

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.ShareMaxCaptureFPS(value: Int) as AdvancedSetting<*>)
```

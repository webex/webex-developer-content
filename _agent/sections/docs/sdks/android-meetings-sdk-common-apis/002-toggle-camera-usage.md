---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-common-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Toggle Camera Usage
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-common-apis). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-common-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides an overview of the common APIs used to implement Webex functionality in your Android application.

---

It covers essential configurations such as setting video frame rates, toggling camera usage, enabling background video streaming, setting screen sharing frame rates, and configuring noise reduction. These APIs help you optimize the performance and quality of your Webex integration.

## Selected section

## Toggle Camera Usage

Toggle the usage of the `android.hardware.camera2` API:

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.VideoEnableCamera2(value: Boolean) as AdvancedSetting<*>)
```

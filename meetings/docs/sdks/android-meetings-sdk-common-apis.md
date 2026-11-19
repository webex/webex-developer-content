---
type: Guide
title: Android Meetings SDK | Common APIs
display_title: BNR and other Common APIs
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-common-apis
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-common-apis)

This article provides an overview of the common APIs used to implement Webex functionality in your Android application.

---

It covers essential configurations such as setting video frame rates, toggling camera usage, enabling background video streaming, setting screen sharing frame rates, and configuring noise reduction. These APIs help you optimize the performance and quality of your Webex integration.

## Configure the Video Frame Rate

Set the maximum transmission frame rate for video:

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.VideoMaxTxFPS(value: Int) as AdvancedSetting<*>)
```

## Toggle Camera Usage

Toggle the usage of the `android.hardware.camera2` API:

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.VideoEnableCamera2(value: Boolean) as AdvancedSetting<*>)
```

## Enable Background Video Streaming

Continue video streaming when the app is in the background:

```kotlin
webex.phone.enableBackgroundStream(enable: Boolean)
```

## Set the Screen Sharing Frame Rate

Set the maximum capture frame rate for screen sharing:

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.ShareMaxCaptureFPS(value: Int) as AdvancedSetting<*>)
```

## Enable/Disable and Configure Noise Reduction

Enable or disable background noise removal:

```kotlin
webex.phone.enableAudioBNR(enable: Boolean)
```

Configure background noise removal mode:

```kotlin
webex.phone.setAudioBNRMode(mode: Phone.AudioBRNMode)
```

---
type: Guide
title: Android Meetings SDK | Set Bandwidth for Your App
display_title: Set Bandwidth
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-set-bandwidth-for-your-app
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-set-bandwidth-for-your-app)

This article explains how to configure the maximum bandwidth for video, audio, and content sharing in your application using the Webex Android SDK.

---

By setting these parameters, you can optimize the quality and performance of media streams according to your application's requirements.



> **Info**
>
> Bandwidth is specified in kilobits per second (kbps).



```kotlin
phone.setAudioMaxBandwidth(64000); // 64kbps for voice
phone.setVideoMaxBandwidth(2000000); // 2Mbps for 1280x720 720p resolution
phone.setShareMaxBandwidth(4000000); // 4Mbps for content share
```



> **Info**
>
> The SDK uses the TIAS (Transport Independent Application Specific) maximum bandwidth modifier in the Session Description Protocol (SDP) to implement this functionality. For more details, please see [RFC3890](https://tools.ietf.org/html/rfc3890).

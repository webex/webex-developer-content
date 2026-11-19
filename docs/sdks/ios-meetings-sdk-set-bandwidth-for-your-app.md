---
type: Guide
title: iOS Meetings SDK | Set Bandwidth for Your App
display_title: Set Bandwidth
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-set-bandwidth-for-your-app
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-set-bandwidth-for-your-app)

To optimize your iOS app's performance you can set bandwidth constraints using the iOS Meetings SDK.

---

To specify the maximum bandwidth used by video, audio and screen sharing, configure the following instance variables:

```swift
phone.audioMaxBandwidth = 64000 // 64kbps
phone.videoMaxBandwidth = 2000000 // 2Mbps for 1280x720 resolution
```



> **Info**
>
> The bandwidth unit of measure is kilobytes per second (kbps).



The SDK uses the TIAS (Transport Independent Application Specific) maximum bandwidth modifier in the SDP to implement this functionality. For more details, please see [RFC3890](https://tools.ietf.org/html/rfc3890).

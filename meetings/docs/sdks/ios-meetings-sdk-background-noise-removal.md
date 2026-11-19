---
type: Guide
title: iOS Meetings SDK | Background Noise Removal
display_title: Background Noise Removal
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-background-noise-removal)

Use the iOS Meetings SDK background noise removal feature (BNR) to improve the quality and clarity of meeting audio.

---

You enable BNR using the `webex.phone.audioBNREnabled` property.

## Enable or Disable BNR

To enable or disable BNR, set `audioBNREnabled` to `true` or `false` as required:

```swift
webex.phone.audioBNREnabled = true // BNR is enabled.
```

## Configure the BNR Mode

The BNR feature supports two modes: Low Power (LP) and High Performance (HP).

```swift
enum AudioBNRMode {
    case LP // Low Power
    case HP // High Performance
}
```

Set the BNR mode to `.HP` by default.



> **Info**
>
> The BNR mode is only effective if `webex.phone.audioBNREnabled` is set to `true`.



```swift
webex.phone.audioBNRMode = .HP
```

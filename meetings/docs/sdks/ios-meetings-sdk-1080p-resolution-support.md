---
type: Guide
title: iOS Meetings SDK | 1080p Resolution Support
display_title: 1080p Support
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-1080p-resolution-support
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-1080p-resolution-support)

Enabling 1080p video resolution (Full HD) is possible for 1-1 calls, space meetings, and Webex meetings by setting the preferred maximum video bandwidth to 1080p.

---



> **Info**
>
> Supported by version 3.5.0 and later of the iOS SDK.



## Capture Full HD Video

To enable full HD video capture:

```swift
webex.phone.videoMaxTxBandwidth = Phone.DefaultBandwidth.maxBandwidth1080p.rawValue
```

## Receive Full HD Video

To enable the reception of full HD video:

```swift
webex.phone.videoMaxRxBandwidth = Phone.DefaultBandwidth.maxBandwidth1080p.rawValue
```

## Important Notes

* Both the sender and receiver must have 1080p video bandwidth enabled to transmit and receive full HD video.
* Video resolution is influenced by:
  * Network bandwidth.
  * Hardware capabilities, including support for hardware codec and sufficient CPU, RAM, and battery.



> **Info**
>
> If you are using the Webex app as remote client and want to utilize 1080p resolution, ensure that the feature is enabled on the client.

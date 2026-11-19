---
type: Guide
title: iOS Meetings SDK | Media Quality Indicators
display_title: Media Quality Indicators
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-media-quality-indicators
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-media-quality-indicators)

Understand media quality during a call or meeting by registering a callback for changes in media quality information.

---

Media Quality Indicator methods provides insights into the network conditions and device status during an active call. It includes notifications for issues like poor uplink, poor downlink, network loss, and confirmation of a good connection.



> **Info**
>
> This feature is available starting from SDK version 3.4.0 onwards.



## Register for Media Quality Updates

To register for media quality updates:

```swift
call.onMediaQualityInfoChanged = { indicator in
    switch indicator {
    case .Good:
               // Quality is good.
    case .PoorUplink:
               // Poor uplink local network condition, e.g., packet loss or jitter between the media server and device while sending media.
    case .PoorDownlink:
               // Poor downlink local network condition, e.g., packet loss or jitter between the media server and device while receiving media.
    case .NetworkLost:
                // Network lost.
    case .DeviceLimitation:
                // The device has poor capability, e.g., insufficient CPU cores or memory size.
    case .HighCpuUsage:
               // The device has high CPU usage.
  }
}
```

![Media quality indicators](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5315582baad0049b/mqi1.gif)

## Unregister from Media Quality Updates

To unregister from meeting quality updates:

```swift
call.onMediaQualityInfoChanged = nil
```

![Unregistered from meeting quality upates](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbcfb44304395bc61/mqi2.gif)

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-media-quality-indicators
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Register for Media Quality Updates
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-media-quality-indicators). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-media-quality-indicators.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Understand media quality during a call or meeting by registering a callback for changes in media quality information.

---

Media Quality Indicator methods provides insights into the network conditions and device status during an active call. It includes notifications for issues like poor uplink, poor downlink, network loss, and confirmation of a good connection.



> **Info**
>
> This feature is available starting from SDK version 3.4.0 onwards.

## Selected section

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

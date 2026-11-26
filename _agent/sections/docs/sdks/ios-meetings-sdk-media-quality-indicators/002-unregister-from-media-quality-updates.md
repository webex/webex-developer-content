---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-media-quality-indicators
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Unregister from Media Quality Updates
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

## Unregister from Media Quality Updates

To unregister from meeting quality updates:

```swift
call.onMediaQualityInfoChanged = nil
```

![Unregistered from meeting quality upates](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbcfb44304395bc61/mqi2.gif)

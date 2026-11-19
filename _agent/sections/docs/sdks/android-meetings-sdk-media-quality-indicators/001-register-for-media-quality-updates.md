---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-media-quality-indicators
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Register for Media Quality Updates
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-media-quality-indicators). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-media-quality-indicators.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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

```kotlin
call.setObserver(object : CallObserver {
        override fun onMediaQualityInfoChanged(mediaQualityInfo: Call.MediaQualityInfo) {
            when (mediaQualityInfo) {
                Call.MediaQualityInfo.NetworkLost -> {
                    // Handle network loss
                }
                Call.MediaQualityInfo.Good -> {
                    // Handle good network quality
                }
                Call.MediaQualityInfo.PoorUplink -> {
                    // Handle poor uplink conditions
                }
                Call.MediaQualityInfo.PoorDownlink -> {
                    // Handle poor downlink conditions
                }
                Call.MediaQualityInfo.HighCpuUsage -> {
                    // Handle high CPU usage
                }
                Call.MediaQualityInfo.DeviceLimitation -> {
                    // Handle device limitations
                }
            }
        }
    })
```

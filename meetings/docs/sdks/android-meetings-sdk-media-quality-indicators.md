---
type: Guide
title: Android Meetings SDK | Media Quality Indicators
display_title: Media Quality Indicators
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-media-quality-indicators
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-media-quality-indicators)

Understand media quality during a call or meeting by registering a callback for changes in media quality information.

---

Media Quality Indicator methods provides insights into the network conditions and device status during an active call. It includes notifications for issues like poor uplink, poor downlink, network loss, and confirmation of a good connection.



> **Info**
>
> This feature is available starting from SDK version 3.4.0 onwards.



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

## Unregister from Media Quality Updates

To unregister from meeting quality updates:

```kotlin
call.setObserver(null)
```

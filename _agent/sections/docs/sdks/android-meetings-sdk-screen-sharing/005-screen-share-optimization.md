---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Screen Share Optimization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-screen-sharing.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex iOS Meetings SDK allows you to share the entire screen of your Android mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own Android application.

## Selected section

## Screen Share Optimization

Screen Share Optimization methods are available to enhance the experience of sharing video and text. These API changes are available from version 3.9.0 onwards.

### Optimization API Examples

The following are examples of how to use the Screen Share Optimization APIs:

1. Screen Sharing on Android devices targeting **API 28** or earlier:

    ```kotlin
    call.startSharing(CompletionHandler { result ->
        if (result.isSuccessful) {
            // startSharing successful
        } else {
            // startSharing failed
        }

    }, shareConfig = ShareConfig((Call.ShareOptimizeType.AutoDetection, false)))
    ```

    The `shareConfig` parameter is optional. If not set, the default optimization with a maximum of 3 fps will be used. The `shareConfig` parameter is available from version 3.9.0 onwards.

2. Screen Sharing on Android devices targeting **API 29** or later:

    ```kotlin
    call.startSharing(notification = buildScreenShareForegroundServiceNotification(), notificationId = 0xabc61. CompletionHandler { result ->
        if (result.isSuccessful) {
            // startSharing successful
        } else {
            // startSharing failed
        } 
    }, shareConfig = ShareConfig((Call.ShareOptimizeType.AutoDetection, false)))

    private fun buildScreenShareForegroundServiceNotification(): Notification {
    
        val channelId =
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
                    createNotificationChannel("screen_share_service_v3_sdk", "Background Screen Share Service v3 SDK")
                } else { "" }
        val notificationBuilder =
                NotificationCompat.Builder(requireContext(), channelId)
                        .setSmallIcon(R.drawable.app_notification_icon)
                        .setContentTitle(getString("ScreenShare"))
                        .setContentText(getString("You are starting screenshare"))
                        .setPriority(NotificationCompat.PRIORITY_MAX)
                        .setTicker(getString(contentId))
                        .setDefaults(Notification.DEFAULT_SOUND)

        return notificationBuilder.build()
    }
    ```

    The `shareConfig` parameter is optional. If not provided, the default optimization is used, and audio is not shared. This parameter has been available since version 3.9.0.

3. To retrieve the current sharing configuration for an active call, use the `call.getShareConfig()` API.

    ```kotlin
    var sharingConfig = call.getShareConfig()
    ```

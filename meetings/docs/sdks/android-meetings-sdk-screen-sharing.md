---
type: Guide
title: Android Meetings SDK | Screen Sharing
display_title: Screen Sharing
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-screen-sharing)

The Webex iOS Meetings SDK allows you to share the entire screen of your Android mobile device during a call or meeting.

---

This article guides your through implementing screen sharing in your own Android application.

## Start Screen Sharing

Before continuing, ensure that the call is in a `CONNECTED` status and that you are not already sharing your screen in this call, otherwise, the callback throws an error.

To start sharing your screen:

```kotlin
activeCall.startSharing(r -> Ln.d("startSharing result: " + r));
```

When initiating screen sharing for the first time, Android displays an alert dialog warning the user that the entire screen will be captured. Checking **Don't show again** prevents this dialog from appearing in the future:

![Share content warning](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt891f4bdfd9f1537e/image2018-3-21_17-23-57.png)

## Stop Screen Sharing

The `SendingSharingEvent` triggers through the `CallObserver.onMediaChanged()` callback after successfully starting or stopping screen sharing. Use the `isSending()` method to check the sharing status:

```kotlin
activeCall.stopSharing(r -> Ln.d("stopSharing result: " + r));
```

## Check the Status of Screen Sharing

To check if screen sharing is active:

```kotlin
boolean isSharing = activeCall.isSendingSharing();
```

## Set the Screen Share View

To view screen or content shared by a remote participant, create a [`MediaOption`](https://ciscospark.github.io/spark-android-sdk/com/ciscospark/androidsdk/phone/MediaOption.html) with the `audioVideoShare` function for the `dial` or `answer` method:

```java
MediaOption option = MediaOption. audioVideoSharing(new Pair<>(localView, remoteView),shareView);

webex.phone().dial("coworker@acm.com", option, (result) -> {
            if (result.isSuccessful()) {
                call = result.getData();
                call.setObserver(callObserver);
            }
            //...
});
```

You can also provide a view only at the point when the other party starts sharing their screen:

```java
MediaOption option = MediaOption. audioVideoSharing(new Pair<>(localView, remoteView),null);

webex.phone().dial("coworker@acm.com", option, (result) -> {
    if (result.isSuccessful()) {
        call = result.getData();
        call.setObserver(callObserver);
    }
    //...
});


@Override
public void onMediaChanged(MediaChangedEvent mediaChangedEvent) {
    if (mediaChangedEvent instanceof RemoteSendingSharingEvent) {
        if (((RemoteSendingSharingEvent) mediaChangedEvent).isSending()) {
            mediaChangedEvent.getCall().setSharingRenderView(shareView);
        } else if (!((RemoteSendingSharingEvent) mediaChangedEvent).isSending()) {
            mediaChangedEvent.getCall().setSharingRenderView(null);
        }
    }
}
```

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

## Set ShareConfig

To set the share configuration, use one of the following options:

```kotlin
    // Default setting: no special optimization, max 3 FPS.    
    var shareConfig = ShareConfig(Call.ShareOptimizeType.Default, false)

    // Auto-detects sharing type, max 5 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.AutoDetection, false)

    // Optimizes screen sharing for video/motion, max 30 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.OptimizeVideo, false)

    // Optimizes video/motion sharing, max 30 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.OptimizeVideo, true)

    // Optimizes text/image sharing, max 5 FPS.
    var shareConfig = ShareConfig(Call.ShareOptimizeType.OptimizeText, false)
```

## ShareMaxCaptureFPS

The `ShareMaxCaptureFPS` method in `AdvancedSetting.kt` allows for setting the maximum fps during screen sharing. However, the Screenshare Optimization settings will override the `ShareMaxCaptureFPS` setting.

```kotlin
webex.phone.setAdvancedSetting(AdvancedSetting.ShareMaxCaptureFPS(fps) as AdvancedSetting<*>)
```

Here are some scenarios showing the interaction between `ShareMaxCaptureFPS` and screenshare optimization from version 3.9.0:

* Set `ShareMaxCaptureFPS` to 10 and `OptimizeText` in `ShareConfig` to limit the FPS to 5.
* Set `ShareMaxCaptureFPS` to 3 and `OptimizeText` in `ShareConfig` to limit the FPS to 5.
* Set `ShareMaxCaptureFPS` to 10 and `OptimizeVideo` in `ShareConfig` to achieve a maximum FPS of 30.
* Set `ShareMaxCaptureFPS` to 7 without using `shareConfig` to achieve a maximum FPS of 7.
* Set `ShareMaxCaptureFPS` to 30 without using `shareConfig` to achieve a maximum FPS of 30.
* Do not set `ShareMaxCaptureFPS` or set it to 0 without using `shareConfig` to limit the FPS to 5.

---
type: Guide
title: Android Meetings SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-quickstart)

This article provides examples of common API usage within the meetings flow. For detailed API information, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance serves as the primary entry point for the SDK, providing access to all Webex SDK APIs. The `Call` object represents a meeting and offers APIs for actions such as joining, leaving, muting, and unmuting. The `Call` object is returned as a result of a successful `dial` API call.

## Join a Meeting

To join a meeting with the `dial` API by providing a meeting ID, SIP address, or meeting link:

```kotlin
webex.phone().dial(meetingId, MediaOption.audioVideoSharing(Pair(localView,remoteView), screenShareView), CompletionHandler { result ->
    if (result.isSuccessful) {
        result.data?.let { _call ->
            // Space call connected. Set observer to listen for call events
            call.setObserver(object : CallObserver {
                override fun onConnected(call: Call?) {
                }

                override fun onRinging(call: Call?) {
                }

                override fun onWaiting(call: Call?, reason: Call.WaitReason?) {
                }

                override fun onDisconnected(event: CallObserver.CallDisconnectedEvent?) {
                }

                override fun onInfoChanged(call: Call?) {
                }

                override fun onMediaChanged(event: CallObserver.MediaChangedEvent?) {
                }

                override fun onCallMembershipChanged(event: CallObserver.CallMembershipChangedEvent?) {
                }

                override fun onScheduleChanged(call: Call?) {
                }
            })
        }
    } else {
        result.error?.let { errorCode ->
            // Error in space call
        }
    }
});
```

## Display Remote Screen Share

To display the screen share from the remote party:

```kotlin
webex.phone.dial("spaceId", MediaOption.audioVideoSharing(Pair(localView, remoteView), screenShareView), CompletionHandler {
    if(it.isSuccessful){
        val call = it.data
        call?.setObserver(object :CallObserver{
            override fun onConnected(call: Call?) {
                super.onConnected(call)
            }

            // ...

            override fun onMediaChanged(event: CallObserver.MediaChangedEvent?) {
                event?.let { _event ->
                    val _call = _event.getCall()
                    when (_event) {
                        is CallObserver.RemoteSendingSharingEvent -> {
                            if (_event.isSending()) {
                                _call?.setSharingRenderView(screenShareView)
                            } else {
                                _call??.setSharingRenderView(null)
                            }
                        }
                    }
                }
            }
        })
    } else {
        val error = it.error
    }
})
```

## Share the Screen from the SDK Client

To start and stop screen sharing:

```kotlin
call.startSharing(CompletionHandler {
if (it.isSuccessful){
    // ...
}
})
call.stopSharing(CompletionHandler {
if (it.isSuccessful){
    // ...
}
})
```

## Check Feature Entitlements

To determine the feature entitlements for messaging, meeting, and calling based on the logged-in user's license:

```kotlin
var capability = webex.people.getProductCapability()

var hasCalling = capability.isCallingSupported()
var hasMessaging = capability.isMessagingSupported()
var hasMeeting = capability.isMeetingSupported()
```

## Manage Background Connection

To maintain the websocket connection in the background for quick synchronization of conversations and meetings:

```kotlin
webex.phone.enableBackgroundConnection(enable: Boolean)
```

## Enable or Disable Console Logging

To toggle console logging:

```kotlin
webex.enableConsoleLogger(enable: Boolean)
```

## Set Log Level

To adjust the log level for debugging purposes:

```kotlin
webex.setLogLevel(logLevel: LogLevel)
```

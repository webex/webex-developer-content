---
type: Guide
title: iOS Meetings SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-quickstart)

This guide provides examples of common methods used in the meetings flow for the iOS Meetings SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the core access point for the SDK, providing access to all Webex SDK methods. A `Call` object represents a meeting and includes methods for joining, leaving, muting, unmuting, and other actions. This object is returned as a result of a successful `dial` method invocation.

## Join a Meeting

Use the `dial` method to join a meeting by passing a meeting ID, SIP address, or meeting link:

```swift
webex.phone.dial("meetingId", option: MediaOption.audioVideo(local: ..., remote: ...)) { result in
    switch result {
    case .success(let call):
        call.onConnected = {
            // ...
        }
        call.onDisconnected = { reason in
            // ...
        }
    case .failure(let error):
        // failure
    }
}
```

## Render Remote Screen Share

To render the screen share from a remote party, use the following code:

```swift
var selfVideoView = MediaRenderView()
var remoteVideoView = MediaRenderView()
var screenShareView = MediaRenderView()
webex.phone.dial("coworker@example.com", option: MediaOption.audioVideoScreenShare(video: (local: selfVideoView, remote: remoteVideoView), screenShare: screenShareView)) { ret in
    switch ret {
    case .success(let call):
        call.onConnected = {
            // ...
        }
        call.onDisconnected = { reason in
            // ...
        }
        call.onMediaChanged = { changed in
            switch changed {
                ...
            case .remoteSendingScreenShare(let sending):
                call.screenShareRenderView = sending ? view : nil
            }
        }
    case .failure(let error):
        // failure
    }
}
```



> **Info**
>
> Screen sharing will only work using v3 SDK with the latest `WebexBroadcastExtensionKit`.



## Set the Composited Video Layout

Change the layout for the active speaker and other attendees' composed video:

```swift
let option: MediaOption = MediaOption.audioVideo(local: ..., remote: ...)
option.compositedVideoLayout = .grid

webex.phone.dial(spaceId, option: option) { ret in
    // ...
}
```

## Verify Feature Entitlements

Features such as messaging, meeting, and calling depend on the logged-in user's license. The `webex.people.getProductCapability()` method verifies a user's entitlements:

```swift
let capability: ProductCapability = webex.people.getProductCapability()
let hasCalling = capability.isCallingSupported
let hasMeeting = capability.isMeetingSupported
let hasMessaging = capability.isMessagingSupported
```

## Manage Background Connections

Maintain the websocket connection in the background to quickly sync conversations and meetings:

```swift
webex.phone.enableBackgroundConnection = true 
```

## Toggle Console Logging

Enable or disable console logging:

```swift
webex.enableConsoleLogger = true    
```

## Set Log Level

Adjust the SDK's log level:

```swift
webex.logLevel = .verbose 
```

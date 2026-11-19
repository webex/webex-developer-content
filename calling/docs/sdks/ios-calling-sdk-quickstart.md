---
type: Guide
title: iOS Calling SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-quickstart)

This guide provides the fundamental steps for integrating calling features into your iOS application using the Webex iOS Mobile SDK. For comprehensive parameters and methods, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

At the core of the SDK is the `Webex` object, serving as the gateway to all SDK functionalities. The `Call` object represents an active call and provides methods to manage various aspects of the call lifecycle, such as answering, hanging up, muting, and unmuting. You obtain a `Call` object either as a result of a successful outgoing call through the `dial` method or as an incoming call event.

## Make an Outgoing Call

To place an outgoing call, use the `dialPhoneNumber` method:

```swift
webex.phone.dialPhoneNumber("+1800123456", option: MediaOption.audioOnly()) { result in
    switch result {
    case .success(let call):
        call.onConnected = {
            // ...
        }
        call.onDisconnected = { reason in
            // ...
        }
    case .failure(let error):
        //call failure
    } 
}
```

## Receive and Answer a Call

Incoming calls are handled by setting a listener on the `onIncoming` event of the `phone` object:

```swift
webex.phone.onIncoming = { call in
    call.answer(option: MediaOption.audioVideo(local: ..., remote: ...)) { error in
    if let error = error {
        // failure
    }
    else {
        // success
    }
}
```

## Determine a User's Calling Type

To determine if the signed-in user is entitled to use Webex Calling, check their calling type:

```swift
if(webex.phone.getCallingType() == Phone.CallingType.WebexCalling){
    // Indicates Webex Calling is supported for signed in user
}
```

## Check Feature Entitlements for the Logged-in User

The user's license dictates their access to messaging, meeting, and calling features. The `webex.people.getProductCapability()` method enables you to verify the user's product capabilities:

```swift
let capability: ProductCapability = webex.people.getProductCapability()
let hasCalling = capability.isCallingSupported
let hasMeeting = capability.isMeetingSupported
let hasMessaging = capability.isMessagingSupported
```

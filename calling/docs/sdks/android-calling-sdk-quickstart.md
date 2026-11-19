---
type: Guide
title: Android Calling SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-quickstart)

This guide provides the fundamental steps for integrating calling features into your Android application using the Webex Android Mobile SDK. For comprehensive parameters and methods, please refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

At the core of the SDK is the `Webex` object, serving as the gateway to all SDK functionalities. The `Call` object represents an active call and provides methods to manage various aspects of the call lifecycle, such as answering, hanging up, muting, and unmuting. You obtain a `Call` object either as a result of a successful outgoing call through the `dial` method or as an incoming call event.



> **Info**
>
> Methods are largely consistent between Unified Communications Manager (UCM) and Webex Calling.



## Make an Outgoing Call

Place an outgoing call using the `dialPhoneNumber()` method:

```kotlin
val mediaOption = MediaOption.audioOnly()
webex.phone.dialPhoneNumber("+1800123456", mediaOption, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Call started successfully; result.data returns a Call object.
    } else {
        // Call failed; result.error returns an error code. The error code is an instance of WebexError.ErrorCode.
    }
})
```

## Receive and Answer an Incoming Call

Set a incoming call listener using the `setIncomingCallListener()` method. If the `Call` object intercepted by the `onIncomingCall()` method is not null, answer it using the `Call` objects's answer method:

```kotlin
webex.phone.setIncomingCallListener(object : Phone.IncomingCallListener {
    override fun onIncomingCall(call: Call?) {
        call?.answer(MediaOption.audioOnly(), CompletionHandler { // use MediaOption.audioVideo() for video webex call. 
            if (it.isSuccessful){
                // The call is answered.
            }
        })
    }
})
```

## Determine a User's Calling Type

Use the `webex.phone.getCallingType()` method to check the calling type associated with the user:

```kotlin
if(webex.phone.getCallingType() == Phone.CallingType.WebexCalling){
    // Indicates Webex Calling is supported for signed in user
}
```

## Check Feature Entitlements for a Logged-In User

The user's license determines their access to meeting, messaging, and calling features. Use `webex.people.getProductCapability()` to verify the user's entitlements.

```kotlin
var capability = webex.people.getProductCapability()

var hasCalling = capability.isCallingSupported()
var hasMessaging = capability.isMessagingSupported()
var hasMeeting = capability.isMeetingSupported()
```

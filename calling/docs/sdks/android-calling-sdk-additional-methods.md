---
type: Guide
title: Android Calling SDK | Additional Methods
display_title: Additional Methods
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-additional-methods)

This article describes additional methods available in the Webex Calling Android SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.



## Sign in and Out of Phone Services

Applications can disconnect from Webex calling phone services, enabling users to cease making and receiving calls while continuing to use other features, such as messaging and meetings.

### Sign in to Phone Services

To sign in to phone services:

```kotlin
webex.phone.connectPhoneServices{ result ->
    if (result.isSuccessful) {
        // Connecting to phone services succeeded
    } else {
        // Connecting to phone services failed
    }
}
```



> **Info**
>
> The actual phone service status is available in the `onUCServerConnectionStateChanged` callback.



### Sign out of phone services

To sign out of phone services:

```kotlin
webex.phone.disconnectPhoneServices{ result ->
    if (result.isSuccessful) {
        // Disconnecting from phone services succeeded
    } else {
        // Disconnecting from phone services failed
    }
}
```



> **Info**
>
> The actual phone service status is available in the `onUCServerConnectionStateChanged` callback.



## Get the Calling Type of a User

The SDK supports various calling types, such as CUCM and WebexCalling. A user is associated with one calling type at most. Use `webex.phone.getCallingType()` method to check the user's calling type:

```kotlin
if(webex.phone.getCallingType() == Phone.CallingType.WebexCalling){
    // Indicates Webex Calling is supported for the signed in user.
}
```

## Get an External Tracking ID

For logging and tracking metrics, use `call.getExternalTrackingId()` to retrieve a tracking ID. This is available in the `onInfoChanged` callback in `CallObserver`.

```kotlin
call.getExternalTrackingId()
// Use the trackingId after the onInfoChanged callback has fired.
```

## Video Enabled in Control Hub

The `isVideoEnabled()` method determines whether video calling is enabled for a user in the Control Hub, affecting the availability of local and remote video features for calls. It is applicable to Locus, CUCM, WebexCalling, and WebexForBroadworks calls only. This setting does not influence video availability for meetings. Available since v3.9.0:

```kotlin
webex.phone.call.isVideoEnabled()
// Returns true if video is enabled for the user in Control Hub or false if not.
```

## Bandwidth Extension / Speech Enhancement

The Bandwidth Extension Support feature allows developers to enhance receiver-side audio quality during WebexCalling and CUCM calls. These APIs are available from SDK v3.14 onwards.

### Phone-Level APIs (Before a Call)

Use these APIs before making a call.

#### Enable Legacy Receiver Noise Removal

```kotlin
// Enable legacy receiver noise removal
webex.phone.useLegacyReceiverNoiseRemoval(true)

// Disable legacy receiver noise removal to use new speech enhancement
webex.phone.useLegacyReceiverNoiseRemoval(false)
```

#### Check if Speech Enhancement Is Enabled by Default

```kotlin
// Check if speech enhancement is enabled by default
var isEnabled = webex.phone.isReceiverSpeechEnhancementEnabled()
```

#### Enable/Disable Speech Enhancement by Default

```kotlin
// Enable speech enhancement by default for all calls
webex.phone.enableReceiverSpeechEnhancement(true) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}

// Disable speech enhancement by default for all calls
webex.phone.enableReceiverSpeechEnhancement(false) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}
```

### Call-Level APIs (During a Call)

Use these APIs while in an active call.

#### Check if Speech Enhancement Is Enabled for the Current Call

```kotlin
// Check if speech enhancement is enabled for the current call
var isEnabled = call.isReceiverSpeechEnhancementEnabled
```

#### Enable/Disable Speech Enhancement for the Current Call

```kotlin
// Enable speech enhancement for the current call
call.enableReceiverSpeechEnhancement(true) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}

// Disable speech enhancement for the current call
call.enableReceiverSpeechEnhancement(false) {
    if (it.isSuccessful) {
        // Speech Enhancement was successfully set
    } else {
        // Handle error
    }
}
```

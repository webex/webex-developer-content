---
type: Guide
title: iOS Calling SDK | Additional Methods
display_title: Additional Methods
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods)

This article describes additional methods available in the Webex Calling iOS SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.



## Sign In to Phone Services

To connect to Webex calling phone services:

```swift
webex.phone.connectPhoneServices(completionHandler: { result in
    switch result {
    case .success:
        // PhoneServices connected successfully.
    case .failure:
        // PhoneServices connection failed.
    }
})
```

The phone service status updates are provided via the `onUCServerConnectionStateChanged` callback.

## Sign Out of Phone Services

To disconnect from Webex calling phone services:

```swift
webex.phone.disconnectPhoneServices(completionHandler: { result in
    switch result {
    case .success:
        // PhoneServices disconnected successfully.
    case .failure:
        // PhoneServices disconnection failure.
    }
})
```

The phone service status updates are provided via the `onUCServerConnectionStateChanged` callback.

## Check the User Calling Type

The SDK supports various calling types, such as CUCM and WebexCalling. A user is associated with one calling type at most. Use `webex.phone.getCallingType()` method to check the user's calling type:

```swift
if(webex.phone.getCallingType() == Phone.CallingType.WebexCalling){
    // Indicates Webex Calling is supported for the signed-in user.
}
```

## External Tracking ID Retrieval

To obtain an `externalTrackingId` for call logging and metrics:

```swift
call.externalTrackingId
// Use the trackingId after the onInfoChanged callback has fired.
```

## Retrieve Video Enabled Status

The `isVideoEnabled()` method determines whether video calling is enabled for a user in the Control Hub, affecting the availability of local and remote video features for calls. It is applicable to Locus, CUCM, WebexCalling, and WebexForBroadworks calls only. This setting does not influence video availability for meetings. Available since v3.9.0:

```swift
let isVideoEnabled = Call.isVideoEnabled
// True if video is enabled, false otherwise.
```

## Bandwidth Extension / Speech Enhancement

The Bandwidth Extension Support feature allows developers to enhance receiver-side audio quality during WebexCalling and CUCM calls. These APIs are available from SDK v3.14 onwards.

### Phone Class APIs (Before a Call)

#### Enable Legacy Receiver Noise Removal

```swift
// Enable legacy receiver noise removal
Webex.phone.useLegacyReceiverNoiseRemoval(useLegacy: true)

// Disable legacy receiver noise removal to use new speech enhancement
Webex.phone.useLegacyReceiverNoiseRemoval(useLegacy: false)
```

#### Check if Speech Enhancement Is Enabled by Default

```swift
// Check if speech enhancement is enabled by default
let isEnabled = Webex.phone.isReceiverSpeechEnhancementEnabled
```

#### Enable/Disable Speech Enhancement by Default

```swift
// Enable speech enhancement by default for all calls
Webex.phone.enableReceiverSpeechEnhancement(shouldEnable: true) { result in
    switch result {
    case .success:
        print("Speech enhancement enabled by default")
    case .failure(let error):
        print("Failed to enable speech enhancement: \(error)")
    }
}

// Disable speech enhancement by default for all calls
Webex.phone.enableReceiverSpeechEnhancement(shouldEnable: false) { result in
    switch result {
    case .success:
        print("Speech enhancement disabled by default")
    case .failure(let error):
        print("Failed to disable speech enhancement: \(error)")
    }
}
```

### Call Class APIs (During a Call)

#### Check if Speech Enhancement Is Enabled for the Current Call

```swift
// Check if speech enhancement is enabled for the current call
let isEnabled = Webex.call.isReceiverSpeechEnhancementEnabled
```

#### Enable/Disable Speech Enhancement for the Current Call

```swift
// Enable speech enhancement for the current call
Webex.call.enableReceiverSpeechEnhancement(shouldEnable: true) { result in
    switch result {
    case .success:
        print("Speech enhancement enabled for the call")
    case .failure(let error):
        print("Failed to enable speech enhancement: \(error)")
    }
}

// Disable speech enhancement for the current call
Webex.call.enableReceiverSpeechEnhancement(shouldEnable: false) { result in
    switch result {
    case .success:
        print("Speech enhancement disabled for the call")
    case .failure(let error):
        print("Failed to disable speech enhancement: \(error)")
    }
}
```

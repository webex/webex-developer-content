---
type: Guide
title: iOS Calling SDK | Basic Webex Calling Usage
display_title: Basic Usage
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-basic-webex-calling-usage)

This article outlines the fundamental steps for integrating call functionality using the Webex iOS SDK.

## Register for Callbacks

To initiate and receive calls, the phone services must be operational. After signing into Webex, authentication for Webex calling phone services occurs automatically via Single Sign-On (SSO). An application can register the `WebexUCLoginDelegate` to determine when the phone services are ready. The `onUCServerConnectionStateChanged` callback indicates the connection status of the phone services, showing `UCLoginServerConnectionStatus.Connected` when available for use:

```swift
class YourViewController: UIViewController {
    override func viewDidAppear(_ animated: Bool) {
        // You need to register your class as a delegate.
        webex.ucLoginDelegate = self
    }
}

extension HomeViewController: WebexUCLoginDelegate {
    func onUCLoggedIn() {
        // Login is successful.
    }
    
    func onUCLoginFailed() {
        // Login attempt failed.
    }
    
    func onUCServerConnectionStateChanged(status: UCLoginServerConnectionStatus, failureReason: PhoneServiceRegistrationFailureReason) {
        if status == .Connected {
            // Server connection success.
        }
    }
    
    func showUCSSOLoginView(to url: String) {
        webex.getUCSSOLoginView(parentViewController: self, ssoUrl: url) { success in
            if let success = success, success {
                // You're logged in.
            }
        }
    }
    
    func showUCNonSSOLoginView() {
        webex.setCallServiceCredential(username: "user@example.com", password: "SuperSecret")
    }
}
```

## Query Phone Services Status

To check the current status of phone services, use the `webex.getUCServerConnectionStatus()` method:

```swift
let phoneServicesStatus = webex.getUCServerConnectionStatus()
if (phoneServicesStatus == UCLoginServerConnectionStatus.Connected) {
    // Indicates that phone services are ready.
}
```

## Place an Outgoing Call

When phone services are active, you can make outgoing calls to any Webex calling or PSTN number using `webex.phone.dialPhoneNumber()`. Note that attempting to dial non-phone numbers with `webex.phone.dialPhoneNumber()` will lead to a call failure, indicated by `INVALID_API_ERROR`:

```swift
webex.phone.dialPhoneNumber("+1800123456", option: MediaOption.audioOnly()) { result in
    switch result {
    case .success(let call):
        call.onConnected = {
            // Do something once the call is connected.
        }
        call.onDisconnected = { reason in
            // Do something on call disconnect.
        }
    case .failure(let error):
        // Call failure.
    } 
}
```



> **Info**
>
> The `dialPhoneNumber` method is available from version 3.9.2 and later.



## Mute or Unmute a Call

Mute a call:

```swift
call?.sendingAudio = false 
```

Unmute a call:

```swift
call?.sendingAudio = true 
```

## Hold or Resume a Call

Hold a call:

```swift
call.holdCall(putOnHold: true) { error in 
    if(error != nil) {
        // hold success
    }
}
```

Resume a call:

```swift
call.holdCall(putOnHold: false) { error in 
    if(error != nil) {
        // Resume success
    }
}
```

Check if a call is on hold:

```swift
let isOnHold = call?.isOnHold()
```

## End a call

End a connected call using the `call.hangup()` method:

```swift
call.hangup(completionHandler: { error in
    if error == nil {
        // Call ended successfully.
    }
    else {
        // Failed to end call.
    }
})
```

## Call history

The SDK provides call history functionality to retrieve, manage, and monitor call records from One-to-One direct calls.
    
1. Get call history records
    ```swift
    // Returns a collection of CallHistoryRecord objects containing
    let callHistoryItems = webex.phone.getCallHistory()
    ```

2. Remove call history records
   ```swift
   // Removes specific call history records using their unique identifiers
   // Use the record IDs obtained from getCallHistory() or event callbacks
   webex.phone.removeCallHistoryRecords(recordIds: [recordIdToDelete])
   ```

3. Register for call history events
   ```swift
   webex.phone.onCallHistoryEvent = { [weak self] (event) in
       switch event {
       case .syncCompleted:
           // Call history synchronization completed
       case .removed(let recordIds):
           // Call history records removed successfully
       case .removeFailed:
           // Call history record removal failed
       }
   }
   ```

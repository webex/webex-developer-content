---
type: Guide
title: Android Calling SDK | Basic Webex Calling Usage
display_title: Basic Usage
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-basic-webex-calling-usage)

This article outlines the fundamental steps for integrating call functionality using the Webex Android SDK.

## Register for Callbacks

To initiate and receive calls, the phone services must be operational. After a user signs into Webex, authentication for Webex calling phone services occurs automatically via Single Sign-On (SSO). An application can register the `WebexUCLoginDelegate` to determine when the phone services are ready. The `onUCServerConnectionStateChanged` callback provides the phone services connection status, indicating `UCLoginServerConnectionStatus.Connected` when it is available for use:

```kotlin
private class UCDelegate() : WebexUCLoginDelegate{
    // Triggered when the application needs to hide the WebView that was loaded in `loadSSOViewInBackground`.
    override fun hideUCSSOBrowser() {
        super.hideUCSSOBrowser()
    }

    // Triggered when SSO authentication for the CUCM domain/server is required.
    // The given ssoUrl needs to be loaded in a WebView to start the authentication process.
    // This callback applies only to [com.ciscowebex.androidsdk.phone.Phone.CallingType.CUCM].
    override fun loadUCSSOViewInBackground(ssoUrl: String) {
        super.loadUCSSOViewInBackground(ssoUrl)
    }

    // Notify when the user is successfully logged in to the Webex Calling service.
    override fun onUCLoggedIn() {
        super.onUCLoggedIn()
    }

    // Notify the app whenever the server URL/domain, username, and password are required for authentication.
    // Application needs to display the option for entering required details.
    override fun onUCLoginFailed() {
        super.onUCLoginFailed()
    }

    // Triggered when an SSO login fails.
    override fun onUCSSOLoginFailed(failureReason: UCSSOFailureReason) {
        super.onUCSSOLoginFailed(failureReason)
    }

    // Triggered when the calling service connection status changes.
    override fun onUCServerConnectionStateChanged(status: UCLoginServerConnectionStatus, failureReason: PhoneServiceRegistrationFailureReason) {
        super.onUCServerConnectionStateChanged(status, failureReason)
        
        // UCLoginServerConnectionStatus indicates the phone services connection status.
    }

    // Triggered when the server URL/domain, username and password are required for authentication.
    // Application needs to display the option for entering required details.
    override fun showUCNonSSOLoginView() {
        super.showUCNonSSOLoginView()
    }

    // Triggered when the application needs to show the webview loaded in [loadSSOViewInBackground].
    override fun showUCSSOBrowser() {
        super.showUCSSOBrowser()
    }
}

//Save the delegate object into webex instance to register the callbacks.
...
webex?.delegate = UCDelegate()
...
```

## Query Phone Services Status

Check the current phone services status using the `webex.getUCServerConnectionStatus()` method:

```kotlin
var phoneServicesStatus = webex.getUCServerConnectionStatus()
if (phoneServicesStatus == UCLoginServerConnectionStatus.Connected) {
    // Phone services are ready to use.
}
```

## Place an Outgoing Call

When phone services are active, you can make outgoing calls to any Webex calling or PSTN number using `webex.phone.dialPhoneNumber()`. Note that attempting to dial anything other than phone numbers with `webex.phone.dialPhoneNumber()` will result in a call failure, indicated by `INVALID_API_ERROR`.

```kotlin
val mediaOption = MediaOption.audioOnly()
webex.phone.dialPhoneNumber("+1800123456", mediaOption, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Dial out is successful; result.data returns a Call object.
        // Store the Call object for further use.
        val call = result.data
        call?.setObserver(object : CallObserver {
            override fun onConnected(call: Call?) {
                super.onConnected(call)
            }

            override fun onDisconnected(event: CallObserver.CallDisconnectedEvent?) {
                super.onDisconnected(event)
            }

            override fun onRinging(call: Call?) {
                super.onRinging(call)
            }
        })
    } else {
        // Dialing failed; result.error, an instance of WebexError.ErrorCode, provides more details.
    }
})
```



> **Info**
>
> The `dialPhoneNumber()` method is available from v3.9.2 and later.



## Mute or Unmute a Call

To mute a call:

```kotlin
call?.setSendingAudio(false)
```

To unmute a call:

```kotlin
call?.setSendingAudio(true)
```

## Hold or Resume a Call

To hold a call:

```kotlin
call?.holdCall(true, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Call hold successful
    } else {
        // Call hold failed
    }
})
```

To resume a call:

```kotlin
call?.holdCall(false, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Call hold successful
    } else {
        // Call hold failed
    }
})
```

Check if a call is on hold:

```kotlin
var isOnHold = call?.isOnHold() : false
```

## End a call

End a connected call using the `call.hangup()` method:

```kotlin
call?.hangup(CompletionHandler { result ->
        if (result.isSuccessful) {
            // Call has ended. Handle cleanup.
        } else {
            // Ending the call failed.
        }
    })
```

## Call history

The SDK provides call history functionality to retrieve, manage, and monitor call records from One-to-One direct calls.

1. Get call history records
    ```kotlin
    // Returns a collection of CallHistoryRecord objects containing
    val callHistoryItems = webex.phone.getCallHistory()
    ```

2. Remove call history records
   ```kotlin
   // Removes specific call history records using their unique identifiers
   // Use the record IDs obtained from getCallHistory() or event callbacks
   webex.phone.removeCallHistoryRecords(recordIds: List<String>)
   ```
3. Register for call history events
   ```kotlin
    webex.phone.setOnCallHistoryEventListener { result ->
        if (result.isSuccessful) {
            val event =  result.data
            when (event) {
                is CallHistoryEvent.SyncCompleted -> { /* Call history synchronization completed */ }
                is CallHistoryEvent.Removed -> { /* Call history records removed successfully. use event.data */ }
                is CallHistoryEvent.RemoveFailed -> { /* Call history record removal failed */ }
            }
        }
    } 
   ```

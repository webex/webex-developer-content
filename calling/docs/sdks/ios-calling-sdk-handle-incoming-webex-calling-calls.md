---
type: Guide
title: iOS Calling SDK | Handle Incoming Webex Calling Calls
display_title: Incoming Calls
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls)

This article describes how to handle incoming Webex Calling based calls.

---

The Webex calling system handles incoming calls through webhooks in the SDK environment. Developers register a webhook with a `targetUrl` for their server backend to receive notifications. These notifications are then delivered to mobile apps via APNS (Apple Push Notification Service) or FCM (Firebase Cloud Messaging), enabling the app to manage incoming calls in any state—whether in the foreground, background, or terminated.

The following diagram illustrates how incoming call notifications are delivered.

![Webex calling incoming call overview.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte02db5e591bea323/wxc_incoming_call.png)

## Configure a Webhook for Incoming Calls



> **Warning**
>
> The `telephony_push` webhook resource is behind the `wxc-push-notification-102812` feature toggle and is not available to organizations by default. To request it, open a case with the [Webex Developer Support Team](https://developer.webex.com/support) and ask for `wxc-push-notification-102812` to be enabled for your organization ID. Until it is enabled, the Create a Webhook API rejects the `telephony_push` resource with `400 Bad Request` (`invalid field: resource`).



1. An organization administrator sets up a firehose webhook to monitor `telephony_push` events and alert a designated server URL upon their firing:

    ```json
    {
    "name": "Webex Calling XYZ Firehose",
    "targetUrl": "https://example.com/message-events", // Server URL of the backend server capable of receiving webhook notifications.
    "resource": "telephony_push",
    "event": "updated"
    }
    ```

2. After successfully logging into the mobile app, the app transmits the user's Person ID and push token (APNS or FCM) to the backend server for storage. The backend uses the Person ID to identify the Webex user upon receiving a webhook notification, and the push token to send notifications to the user's device:

    ```swift
    webex.people.getMe(completionHandler: { [weak self] in
        switch $0 {
        case .success(let user):
            let personId = user.encodedId
        case .failure(let error):
            // Error getting current user
        }
    })
    ```

    

> **Info**
>
> To set up Apple Push Notification Service for your iOS app, refer to this [link](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns). To handle VoIP notifications, you need to set up CallKit in your app. Refer to this [link](https://developer.apple.com/documentation/callkit).



3. Upon receiving a webhook notification indicating an incoming call, the backend server uses the `actorId` field to identify the user. It then sends the corresponding `payload—apnsPayload` for iOS to the user's device, leaving the content unchanged.

4. Upon receiving the FCM or APNS payload, the mobile app should forward it to the SDK API for processing.

## Processing the Incoming Call Payload

Here's how an app processes the incoming call notification:

1. **Receive the notification payload:** The `PKPushRegistryDelegate` class's `didReceiveIncomingPushWith` method receives the notification payload. The app verifies that the Webex SDK is initialized and authorized, then sets an incoming call listener before processing the message:

    ```swift
    if type == .voIP {
        // Report the call to CallKit, and let it display the call UI.
        guard let bsft = payload.dictionaryPayload["bsft"] as? [String: Any], let sender = bsft["sender"] as? String else {
        print("payload not valid")
        return
        }
        callKitManager?.reportIncomingCallFor(uuid: UUID(), sender: sender) {
        completion()
        self.establishConnection(payload: payload)
        }
    } 
    ```

2. **Set the incoming call listener and process the message:** The app sets an incoming call listener and processes the push notification message using the `webex.phone.processPushNotification()` method:

    ```swift
    webex.initialize { [weak self] success in
        if success {
            webex.phone.onIncoming = { [weak self] call in
            self?.callKitManager?.updateCall(call: call)
            }
            do {
                let data = try JSONSerialization.data(withJSONObject: payload.dictionaryPayload, options: .prettyPrinted)
                let string = String(data: data, encoding: .utf8) ?? ""
                // Received push.
                webex.phone.processPushNotification(message: string) { error in
                    if let error = error {
                        // processPushNotification error.
                    }
                }
            }
            catch (let error){
                // Error.
            } 
        }
    }
    ```

    ```swift
    func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
        guard let authType = UserDefaults.standard.string(forKey: "loginType") else { return }
        if authType == "jwt" {
            // init Webex using JWT.
        } else if authType == "token" {
            // init Webex using token.
        } else {
            // init Webex using OAuth. 
        }
        DispatchQueue.main.async {
            webex.initialize { success in
                if success {
                    do {
                        let data = try JSONSerialization.data(withJSONObject: userInfo, options: .prettyPrinted)
                        let string = String(data: data, encoding: .utf8) ?? ""
                        // Received push.
                        webex.phone.processPushNotification(message: string)  { error in
                            if let error = error {
                                // processPushNotification error.
                            }
                        }
                    }
                    catch (let error){
                        // error.
                    }
                
                }
            }
        }
    }
    ```

    The application receives an incoming `Call` object through the `Phone.IncomingCallListener` observer, which is set using `webex.phone.onIncoming`.

3. **Answering or rejecting a call:** The app can answer the call using the `answer` API or reject it using the `reject` API:

    ```swift
    call.answer(option: MediaOption.audioOnly(), completionHandler: { error in
        if error != nil {
            ...
        }
    })
    ```

    ```swift
    call?.reject(completionHandler: { error in
        if error == nil {
            // Reject call successful.
        } else {
            // Reject call failed.
        }
    })
    ```

## Call Observer Events

`telephony_push` events from webhooks indicate `NewCall` type notifications, signifying a new incoming call for a particular user.

The app can monitor the following key call state changes:

```swift
call.onConnected = {
    // Indicates call is successfully established.
}
call.onDisconnected = { reason in
    // Indicates call is disconnected.
}
call.onRinging = {
    // Indicates call is placed and is in ringing state.
}
call.onInfoChanged = {
    // Indicates call info is updated.
    // call.externalTrackingId can be used here to retrieve a tracking ID.
}
call.onCallHoldStateChanged = { holdResumeInfo in
     // Indicates call's hold status changed
 }
```

### Key Observer Events

Key events include:

1. `onRinging` : The call is placed, and the remote participant's device is ringing.
2. `onConnected` : The call is successfully established.
3. `onDisconnected` : The call is disconnected; this event is also triggered when the call is answered on another device.
4. `onInfoChanged` : Call details in the `Call` object are updated.
5. `onCallHoldStateChanged` : Indicates call's hold status changed.

## Incoming Call Sequence Diagram

![Incoming call sequence diagram](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt44ffa353c9708dec/ios_sequence_diagram.png)

## Hande Multiple Incoming Calls

Here's a typical scenario for managing two incoming calls:

1. Receive the first incoming call notification.
2. Display the notification to the user.
3. If the user accepts, the first call is active.
4. When a second incoming call notification arrives, display it to the user.
5. If the user accepts the new call:
    * The active call is put on hold.
    * The new call is answered.
6. The user can switch between calls by toggling hold/resume states.
7. Calls can be ended using their respective `call` object.
8. `CallObserver` notifications should be handled to update the UI accordingly.
9. If the user rejects the new call, the active call remains uninterrupted.

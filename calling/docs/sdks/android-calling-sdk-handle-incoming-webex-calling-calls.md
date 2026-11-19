---
type: Guide
title: Android Calling SDK | Handle Incoming Webex Calling Calls
display_title: Incoming Calls
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls)

This article describes how to handle incoming Webex Calling based calls.

---

The Webex calling system integrates incoming call handling via webhooks within the SDK environment. Developers register a webhook by specifying a URL for their server backend to receive notifications. These notifications are typically relayed to mobile apps through APNS (Apple Push Notification Service) or FCM (Firebase Cloud Messaging). This setup enables the app to manage incoming calls regardless of its state—whether in the foreground, background, or even when terminated.

The diagram illustrates how incoming call notifications are delivered.

![Incoming call notification flow.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb76ab2cf913d875b/wxc_incoming_call.png)


## Webhook Configuration for Incoming Calls



> **Warning**
>
> The `telephony_push` webhook resource is behind the `wxc-push-notification-102812` feature toggle and is not available to organizations by default. To request it, open a case with the [Webex Developer Support Team](https://developer.webex.com/support) and ask for `wxc-push-notification-102812` to be enabled for your organization ID. Until it is enabled, the Create a Webhook API rejects the `telephony_push` resource with `400 Bad Request` (`invalid field: resource`).



To configure a webhook for incoming calls:

1. An organization administrator creates a firehose webhook, which listens for `telephony_push` events and notifies a specified server URL when such events occur:

    ```json
    {
        "name": "Webex Calling XYZ Firehose",
        "targetUrl": "https://example.com/message-events", // Server url of backend server that can receive the webhook notification
        "resource": "telephony_push",
        "event": "updated"
    }
    ```

2. Upon successful login, the mobile app sends the user's Person ID and push token (APNS or FCM) to the backend server, where they are stored. The Person ID identifies the Webex user when the backend receives a webhook notification, and the push token is used for sending notifications to the user's device:

    ```kotlin
    webex.people.getMe() { result ->
        val person = result.data
        person?.let {
            // Person id
            val personId = it.encodedId
        }
    }
    ```

    

> **Info**
>
> Instructions for setting up Firebase Cloud Messaging for Android apps can be found [here](https://firebase.google.com/docs/cloud-messaging/android/client).



3. Upon receiving a webhook notification containing a JSON payload that signals an incoming call, the backend server identifies the user through the "actorId" field. It then sends the corresponding payload—`apnsPayload` for iOS and `fcmPayload` for Android—to the user's device, ensuring the content remains unaltered.

4. When the mobile app receives the FCM or APNS payload, it should pass it to the SDK method `processPushMessageInternal()` for further processing.

## Processing the Incoming Call Payload

Here's how an app processes the incoming call notification:

1. **Receive the Notification Payload:** The notification payload is received by the `FirebaseMessagingService` class's `onMessageReceived` method. The app checks if the Webex SDK is initialized and authorized and sets an incoming call listener before processing the message:

    ```kotlin
        val authorized = webex.authenticator?.isAuthorized()
        if (authorized == true) { // SDK is initialized and authorized.
            processPushMessageInternal(fcmDataPayload) {
                if (it.isSuccessful && it.data == PushNotificationResult.NoError) {
                    // Successfully sent the payload to the SDK.
                }
            }
        } else { // SDK is not initialized. Application might have killed.
            webex.initialize {
                if (webex.authenticator?.isAuthorized() == true) {
                    processPushMessageInternal(fcmDataPayload) {
                        if (it.isSuccessful && it.data == PushNotificationResult.NoError) {
                            // Successfully sent the payload to the SDK.
                        }
                    }
                }
            }
        }
    ```

2. **Set Incoming Call Listener and Process the Message:** The app sets an incoming call listener and processes the push notification message using the `webex.phone.processPushNotification()` method:

    ```kotlin
        private fun processPushMessageInternal(msg :String, handler: CompletionHandler<PushNotificationResult>) {
            // SDK Methods
            if(!notRegistered){
                webex.phone.setIncomingCallListener(object : Phone.IncomingCallListener {
                    override fun onIncomingCall(call: Call?) {
                        // Using this call object, the call can be answered.
                    }
                })
            }

            // SDK method to process the push message.
            webex.phone.processPushNotification(msg) {
                if (it.isSuccessful) {
                    // Successfully sent the payload to the SDK.
                    if (it.data == PushNotificationResult.NoError) {
                        handler.onComplete(ResultImpl.success(PushNotificationResult.NoError))
                    }
                    else {
                        // Handle the error. 
                    }
                }
            }
        }
    ```

    The application receives an incoming `Call` object in the observer `Phone.IncomingCallListener` which is initialized  using `webex.phone.setIncomingCallListener`.

3. **Answering or Rejecting a Call:** The app can answer the call using the `answer()` method or reject it using the `reject()` method:

    ```kotlin
    call?.answer(MediaOption.audioOnly(), CompletionHandler {
        if (it.isSuccessful){
            // Call answered successfully.
        } else {
            // Call answer failed.
        }
    })
    ```

    ```kotlin
    call?.reject { result ->
        if (result.isSuccessful) {
            // Call rejected successfully.
        } else {
            // Call reject failed. 
        }
    }
    ```

## Call Observer Events

`telephony_push` events from webhooks indicate `NewCall` type notifications, signifying a new incoming call for a particular user.

The app can monitor the following key call state changes:

```kotlin
call?.setObserver(object : CallObserver {
    override fun onConnected(call: Call?) {
        // Indicates call is successfully established.
    }

    override fun onDisconnected(event: CallObserver.CallDisconnectedEvent?) {
        // Indicates call is disconnected.
    }

    override fun onRinging(call: Call?) {
        // Indicates call is placed and is in ringing state.
    }

    override fun onInfoChanged(call: Call?) {
        // Indicates call info is updated.
        // call.getExternalTrackingId() can be used to retrieve the tracking ID.
    }

    override fun onCallHoldStateChanged(call: Call?, holdResumeInfo: HoldResumeInfo) {
        // Indicates if the call's hold state has changed
    }
})
```

### Key Observer Events

Key events include:

1. `onRinging` : The call is placed, and the remote participant's device is ringing.
2. `onConnected` : The call is successfully established.
3. `onDisconnected` : The call is disconnected; this event is also triggered when the call is answered on another device.
4. `onInfoChanged` : Call details in the `Call` object are updated.
5. `onCallHoldStateChanged`: Indicates that the hold state of the call has changed.

## Incoming Call Sequence Diagram

![Incoming call flow.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8c70eb4c3f474258/fcm_sequence_diagram.png)

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

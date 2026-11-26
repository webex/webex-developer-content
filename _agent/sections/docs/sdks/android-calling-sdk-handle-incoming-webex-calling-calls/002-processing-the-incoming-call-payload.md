---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Processing the Incoming Call Payload
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes how to handle incoming Webex Calling based calls.

---

The Webex calling system integrates incoming call handling via webhooks within the SDK environment. Developers register a webhook by specifying a URL for their server backend to receive notifications. These notifications are typically relayed to mobile apps through APNS (Apple Push Notification Service) or FCM (Firebase Cloud Messaging). This setup enables the app to manage incoming calls regardless of its state—whether in the foreground, background, or even when terminated.

The diagram illustrates how incoming call notifications are delivered.

![Incoming call notification flow.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb76ab2cf913d875b/wxc_incoming_call.png)

## Selected section

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

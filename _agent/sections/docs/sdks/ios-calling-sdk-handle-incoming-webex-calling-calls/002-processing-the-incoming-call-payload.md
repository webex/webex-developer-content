---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Processing the Incoming Call Payload
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes how to handle incoming Webex Calling based calls.

---

The Webex calling system handles incoming calls through webhooks in the SDK environment. Developers register a webhook with a `targetUrl` for their server backend to receive notifications. These notifications are then delivered to mobile apps via APNS (Apple Push Notification Service) or FCM (Firebase Cloud Messaging), enabling the app to manage incoming calls in any state—whether in the foreground, background, or terminated.

The following diagram illustrates how incoming call notifications are delivered.

![Webex calling incoming call overview.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte02db5e591bea323/wxc_incoming_call.png)

## Selected section

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

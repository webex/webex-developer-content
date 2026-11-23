---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Configuration for Incoming Calls
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

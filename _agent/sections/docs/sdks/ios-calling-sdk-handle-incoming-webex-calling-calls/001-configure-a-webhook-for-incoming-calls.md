---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure a Webhook for Incoming Calls
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

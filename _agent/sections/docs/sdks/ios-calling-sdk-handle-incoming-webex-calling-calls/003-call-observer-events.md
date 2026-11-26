---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Observer Events
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

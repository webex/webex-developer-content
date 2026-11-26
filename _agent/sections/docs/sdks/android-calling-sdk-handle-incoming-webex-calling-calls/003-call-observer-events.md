---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Observer Events
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

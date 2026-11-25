---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Hande Multiple Incoming Calls
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

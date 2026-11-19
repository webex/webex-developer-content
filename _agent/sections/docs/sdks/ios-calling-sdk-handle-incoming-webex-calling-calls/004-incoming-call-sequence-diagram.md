---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-handle-incoming-webex-calling-calls
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Incoming Call Sequence Diagram
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

## Incoming Call Sequence Diagram

![Incoming call sequence diagram](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt44ffa353c9708dec/ios_sequence_diagram.png)

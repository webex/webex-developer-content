---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Intercept Messaging Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/ios-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the core access point for the SDK, providing access to all Webex SDK methods.

## Selected section

## Intercept Messaging Events

To intercept messaging events:

```swift
webex.messages.onEvent = { messageEvent in
    switch messageEvent{
    case .messageReceived(let message):
        // ...
    case .messageDeleted(let messageId):
        // ...
    }
}
```

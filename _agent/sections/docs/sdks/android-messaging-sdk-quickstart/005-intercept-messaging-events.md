---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Intercept Messaging Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the primary entry point for the SDK, allowing access to all Webex SDK APIs.

## Selected section

## Intercept Messaging Events

To intercept messaging events:

```kotlin
webex.messages.setMessageObserver(object : MessageObserver {
    override fun onEvent(event: MessageObserver.MessageEvent) {
        when (event) {
            is MessageObserver.MessageReceived -> {
                val message = event.getMessage()
                if (message?.getParentId() != null) {
                    // Threaded message
                }
            }
            is MessageObserver.MessageDeleted -> {
                // message deleted
            }
            is MessageObserver.MessageFileThumbnailsUpdated -> {
                // thumbnails updated for files
            }
            is MessageObserver.MessageEdited -> {
                // message edited successfully. event.getMessage() returns the edited message.
            }
        }
    }
})
```

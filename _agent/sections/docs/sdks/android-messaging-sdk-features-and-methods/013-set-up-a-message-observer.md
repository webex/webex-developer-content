---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Set Up a Message Observer
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Set Up a Message Observer

To set up a message observer to receive messaging events:

```kotlin
webex.messages.setMessageObserver(object : MessageObserver {
    override fun onEvent(event: MessageObserver.MessageEvent) {
        when (event) {
            is MessageObserver.MessageReceived -> {
                // event.getMessage() gives the Message object
            }
            is MessageObserver.MessageDeleted -> {
                ...
            }
            is MessageObserver.MessageFileThumbnailsUpdated -> {
                ...
            }
            is MessageObserver.MessageEdited -> {
                ...
            }
            is MessageObserver.MessagesUpdated -> {
                ...
            }
        }
    }
})
```

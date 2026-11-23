---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Delete a Message
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Delete a Message

To delete a message using it message ID:

```kotlin
webex.messages.delete(messageId, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Message deleted successfully
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

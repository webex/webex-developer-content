---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- List Messages Before a Specific Date
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## List Messages Before a Specific Date

To retrieve messages in a space before a given date:

```kotlin
val before = Before.Date(date)
webex.messages.list(spaceId, before, max, mentions, { result ->
    if (result.isSuccessful) {
        // result.data contains the messages
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```



> **Info**
>
> Specify the maximum number of messages to return using `max`.

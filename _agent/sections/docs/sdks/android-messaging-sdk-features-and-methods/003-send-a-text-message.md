---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Send a Text Message
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Send a Text Message

Send a text messages to a person via ID or email, or to a space:

```kotlin
webex.messages.postToPerson(personId, message, null, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Success. result.data contains the Message object
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

```kotlin
val emailAddress = EmailAddress.fromString(email) // email is the Email address in string format
webex.messages.postToPerson(emailAddress, message, files, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Success. result.data contains the Message object
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

```kotlin
val text: Message.Text = Message.Text.plain("some_message")
webex.messages.postToSpace(spaceId, text, null, null, CompletionHandler { result ->
    if (result.isSuccessful) {
        // Success. result.data contains the Message object
    } else {
        // Error occurred. result.error?.errorMessage provides the error message
    }
})
```

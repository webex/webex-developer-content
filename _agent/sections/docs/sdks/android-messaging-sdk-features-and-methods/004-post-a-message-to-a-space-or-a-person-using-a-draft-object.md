---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Post a Message to a Space or a Person using a Draft object
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Post a Message to a Space or a Person using a Draft object

The `target` is the destination to which the message is being sent and can be a person ID, space ID, or email address. The `draft` is of type [Message.Draft](https://webex.github.io/webex-android-sdk/-s-d-k/com.ciscowebex.androidsdk.message/-message/-draft/index.html?query=interface%20Draft).

To post a message to a space or person using a draft object:

```kotlin
webex.messages.post(target, draft, CompletionHandler { result ->
    if (result.isSuccessful) {
        // result.data contains the message object
    } else {
        // result.error?.errorMessage gives the error message
    }
})
```

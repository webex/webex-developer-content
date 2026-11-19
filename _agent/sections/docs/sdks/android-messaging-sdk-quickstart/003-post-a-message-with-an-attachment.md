---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Post a Message with an Attachment
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the primary entry point for the SDK, allowing access to all Webex SDK APIs.

## Selected section

## Post a Message with an Attachment

To post a message to a space with an attachment:

```kotlin

// targetId is the spaceId or personId or email address

webex.messages.post(targetId, Message.draft(Message.Text.markdown("**Hello**", null, null)).addAttachments(localFile), CompletionHandler { result ->
    if (result.isSuccessful) {
        // message sent successfully
    } else {
        val error = result.error
        // message sent failed
    }
})
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add a User to a Space
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides examples of common methods used in the meetings flow for the iOS Messaging SDK. For detailed method parameters, refer to the [SDK API Reference](https://developer.webex.com/docs/sdks/android-sdk-overview#sdk-api-reference).

---

The `Webex` instance is the primary entry point for the SDK, allowing access to all Webex SDK APIs.

## Selected section

## Add a User to a Space

To add a user to a space:

```kotlin
webex.memberships.create(space.id, null, "person@example.com", true, CompletionHandler<Membership?> { result ->
    if (result.isSuccessful) {
        val space = result.data
    } else {
        val error= result.error
    }
})
```

### Post a Message in a Space

To post a message in the space:

```kotlin
webex.messages.postToSpace(space.id, Message.Text.plain("Hello"), null, null, CompletionHandler<Message> { result ->
    if(result != null && result.isSuccessful){
        val message = result.data
    }
})
```

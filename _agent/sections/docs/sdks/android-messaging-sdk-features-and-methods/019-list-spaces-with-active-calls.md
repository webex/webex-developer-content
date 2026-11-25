---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- List Spaces with Active Calls
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## List Spaces with Active Calls

To get a list of spaces that currently have an ongoing call:

```kotlin
webex.spaces.listWithActiveCalls(CompletionHandler { result ->
    if (result.isSuccessful) {
        // callback returned success, result.data gives data if any
    } else {
        // callback returned failure
    }
})
```

### Check for 'All' Mentions in a Message

To determine if a message mentions all participants in a space:

```kotlin
message.isAllMentioned()
```

### Retrieve a List of Mentioned People in a Message

To retrieve a list of people mentioned in a message:

```kotlin
var mentions = message.getMentions()
```

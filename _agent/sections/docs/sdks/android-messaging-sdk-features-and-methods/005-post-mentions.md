---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Post Mentions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-features-and-methods). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-features-and-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides detailed information on the messaging features and methods provided by the Webex Android Messaging SDK.

---

The SDK lets you easily implement real-time messaging capabilities including posting new messages, and deleting, listing, and editing existing messages.

## Selected section

## Post Mentions

To post a message mentioning a particular person using a person ID:

```kotlin
// Mention individuals
val mentionsList = ArrayList<Mention>()
mentionsList.add(Mention.Person("personId1", startIndex, endIndex))
mentionsList.add(Mention.Person("personId2", startIndex, endIndex))
webex.messages.postToSpace(spaceId, text, mentionsList, files, completionHandler)
```

To post a mention to a group:

```kotlin
// Mention groups
val mentionsList = ArrayList<Mention>()
mentionsList.add(Mention.All())
webex.messages.postToSpace(spaceId, text, mentionsList, files, completionHandler)
```



> **Info**
>
> The `startIndex` and `endIndex` are the index positions in the text message which will indicate the mention object. For example, to mention **XYZ** in the text `Hello XYZ`, the index position would be 6 and 8, where 6 is the `startIndex` and 8 is the `endIndex`.

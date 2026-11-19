---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-monitor-presence
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Begin Monitoring Presence
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-messaging-sdk-monitor-presence). [Full Markdown](../../../../../docs/sdks/android-messaging-sdk-monitor-presence.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Presence Status provides real-time status updates about contacts which include predefined states, custom messages and state-specific expiration and last active times.

---

The presence related methods can be accessed through the `PersonClient` object.



> **Info**
>
> Available starting from SDK version 3.10.0.

## Selected section

## Begin Monitoring Presence

To monitor presence updates for contacts, use the `webex.people.startWatchingPresences()` method:

```kotlin
val contactIds = listOf("ContactId1", "ContactId2")
val presenceHandles = webex.people.startWatchingPresences(contactIds) { presence ->
    // Handle presence updates
    println("Updated presence for ${presence.getContactId()}: ${presence.getStatus()}")
}
```

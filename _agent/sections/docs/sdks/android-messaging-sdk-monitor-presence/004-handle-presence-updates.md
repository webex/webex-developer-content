---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-monitor-presence
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle Presence Updates
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

## Handle Presence Updates

Upon receiving a presence update, use the `Presence` struct to manage and display the returned information.

Be sure to check `expiresTime` for statuses like DND, OutOfOffice, etc., and use `lastActiveTime()` to display how long a user has been inactive:

```kotlin
val presenceHandles = webex.people.startWatchingPresences(contactIds) { presence ->
    println("Contact: ${presence.getContactId()}")
    println("Status: ${presence.getStatus()}")
    println("Custom Message: ${presence.getCustomStatus()}")
    
    if (presence.getStatus() == PresenceStatus.Inactive) {
        println("Last active: ${presence.getLastActiveTime()}ms ago")
    }

    if (presence.getStatus() in listOf(PresenceStatus.Dnd, PresenceStatus.OutOfOffice, PresenceStatus.Quiet)) {
        println("Status expires in: ${presence.getExpiresTime()}ms")
    }
}
```

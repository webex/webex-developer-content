---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-monitor-presence
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle Presence Updates
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-messaging-sdk-monitor-presence). [Full Markdown](../../../../../docs/sdks/ios-messaging-sdk-monitor-presence.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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

```swift
let presenceHandles = webex.people.startWatchingPresences(contactIds: contactIds, completionHandler: { presence in
    // Handle presence updates
    print("Contact: \(presence.contactId)")
    print("Status: \(presence.status}")
    print("Custom Message: \(customStatus)")
    
    if presence.status == PresenceStatus.Inactive {
        print("Last active: (\presence.lastActiveTime)ms ago")
    }

    if [PresenceStatus.OutOfOffice, PresenceStatus.Dnd, PresenceStatus.Quiet].contains(presence.status)
    {
        print("Status expires in: \(presence.expiresTime)ms")                     
    }
}
```

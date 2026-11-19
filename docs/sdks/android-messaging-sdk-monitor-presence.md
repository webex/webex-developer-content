---
type: Guide
title: Android Messaging SDK | Monitor Presence
display_title: Monitor Presence
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-monitor-presence
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-messaging-sdk-monitor-presence)

Presence Status provides real-time status updates about contacts which include predefined states, custom messages and state-specific expiration and last active times.

---

The presence related methods can be accessed through the `PersonClient` object.



> **Info**
>
> Available starting from SDK version 3.10.0.



## Key Components

Following are the key methods, and statuses provided for presence monitoring:

- **PresenceHandle**
  - `getHandle(): Long`: Returns the unique handle identifier associated with each `contactID`.
  - `getContactId(): String`: Returns the contact ID.
  - `isValid(): Boolean`: Indicates if the handle is valid, returning `false` for invalid or bot contact IDs.

- **Presence**
  - `getContactId(): String`: Returns the contact ID associated with this presence status.
  - `getStatus(): PresenceStatus`: Returns the current presence status.
  - `getCustomStatus(): String`: Returns a custom status message if set by the user.
  - `getLastActiveTime(): Long`: Returns the last active UTC time in milliseconds.
  - `getExpiresTime(): Long`: Returns the status expiration UTC time in milliseconds for states like DND, OutOfOffice, etc.

- **Presence States**

  - Unknown
  - Pending
  - Active
  - Inactive
  - DND (Do Not Disturb)
  - Quiet
  - Busy
  - OutOfOffice
  - Call
  - Meeting
  - Presenting
  - CalendarItem


## Begin Monitoring Presence

To monitor presence updates for contacts, use the `webex.people.startWatchingPresences()` method:

```kotlin
val contactIds = listOf("ContactId1", "ContactId2")
val presenceHandles = webex.people.startWatchingPresences(contactIds) { presence ->
    // Handle presence updates
    println("Updated presence for ${presence.getContactId()}: ${presence.getStatus()}")
}
```

## Stop Watching Presence

To stop presence updates use the `webex.people.stopWatchingPresences()` method, passing in presence handles:

```kotlin
webex.people.stopWatchingPresences(presenceHandles)
```

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

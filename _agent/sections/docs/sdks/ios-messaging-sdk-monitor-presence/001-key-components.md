---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-messaging-sdk-monitor-presence
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Key Components
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

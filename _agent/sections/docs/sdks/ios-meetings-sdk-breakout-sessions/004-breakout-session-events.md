---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Breakout Session Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions). [Full Markdown](../../../../../docs/sdks/ios-meetings-sdk-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Breakout sessions allow meeting participants to join smaller groups within a meeting, facilitated by the meeting host or co-host. Attendees can join or leave these sessions if they are granted permission.

---



> **Info**
>
> Available from SDK v3.7.0 onwards.





> **Info**
>
> Currently, attendee support is provided, but host controls, such as creating or editing a session, are not supported.

## Selected section

## Breakout Session Events

### 1. Session Enabled

Triggered when breakout sessions are enabled for a meeting:

```swift
webex.phone.call.onSessionEnabled
```

### 2. Session Started

Occurs when a breakout session starts, returning a breakout object with session info:

```swift
webex.phone.call.onSessionStarted(breakout: Breakout)
```

### 3. Session Joined

Occurs when an attendee joins a breakout session, either manually or when assigned and started by the host:

```swift
webex.phone.call.onSessionJoined(breakoutSession: BreakoutSession)
```

### 4. Breakout Sessions List Updated

Triggered when the list of joinable breakout sessions for an attendee is updated:

```swift
webex.phone.call.onJoinableSessionUpdated(breakoutSessions: List<BreakoutSession>)
```

### 5. Breakout updated

Triggered when breakout settings are updated:

```swift
webex.phone.call.onBreakoutUpdated(breakout: Breakout)
```

### 6. Joined Session Updated

Triggered when the breakout session an attendee has joined is updated:

```swift
webex.phone.call.onJoinedSessionUpdated(breakoutSession: BreakoutSession)
```

### 7. Broadcast Message Received

Occurs when a broadcast message from the host is received by the participant in a session:

```swift
webex.phone.call.onBroadcastMessageReceivedFromHost(message: String)
```

### 8. Host Asking To Return To Main Session

Triggered when the host requests participants to return to the main meeting:

```swift
webex.phone.call.onHostAskingReturnToMainSession
```

### 9. Session Closing

Occurs when the breakout session is about to close, either immediately or after a delay configured by the host or co-host. The delay can be retrieved using the `Breakout.getDelay()` method:

```swift
webex.phone.call.onSessionClosing
```

### 10. Returned to Main Session

Triggered when a participant returns to the main session:

```swift
webex.phone.call.onReturnedToMainSession
```

### 11. Error Occurred

Triggered when an error occurs while joining a session or returning to the main session:

```swift
webex.phone.call.onBreakoutErrorHappened(BreakoutError)
```

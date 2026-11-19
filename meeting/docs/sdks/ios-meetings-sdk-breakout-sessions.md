---
type: Guide
title: iOS Meetings SDK | Breakout Sessions
display_title: Breakout Sessions
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions)

Breakout sessions allow meeting participants to join smaller groups within a meeting, facilitated by the meeting host or co-host. Attendees can join or leave these sessions if they are granted permission.

---



> **Info**
>
> Available from SDK v3.7.0 onwards.





> **Info**
>
> Currently, attendee support is provided, but host controls, such as creating or editing a session, are not supported.



## Breakout

Represents the settings/information for all the Breakout Sessions configured by the host/co-host.

### 1. startTime: Date

The start time of the breakout sessions.

### 2. duration: Double

The duration of the breakout sessions in seconds.

### 3. delay: Double

The delay time in seconds before the breakout sessions are ended after the closing process starts.

### 4. allowReturnToMainSession: Bool

Indicates whether participants can return to the main session after the breakout sessions are closed.

### 5. canJoinLater: Bool

Determines if participants can join the session later.

## BreakoutSession

Contains information for a specific breakout session.

### 1. name: String

The name of the breakout session.

### 2. sessionId: String

The unique session ID of the breakout session.

### 3. isAssigned: Bool

Indicates if the session is assigned by the host or co-host.

## Attendee Support Methods

This section describes attendee support methods.

### Join/Leave Breakout Session

Join a breakout session.

```swift
webex.phone.joinBreakoutSession(breakoutSession: BreakoutSession)
```

Return to the main session.

```swift
webex.phone.returnToMainSession()
```

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

---
type: Guide
title: Android Meetings SDK | Breakout Sessions
display_title: Breakout Sessions
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-breakout-sessions
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-breakout-sessions)

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

### 1. getStartTime(): Long

The start time of the breakout sessions.

### 2. getDuration(): Long

The duration of the breakout sessions in seconds.

### 3. getDelay(): Long

The delay time in seconds before the breakout sessions are ended after the closing process starts.

### 4. allowReturnToMainSession(): Boolean

Indicates whether participants can return to the main session after the breakout sessions are closed.

### 5. allowJoinLater(): Boolean

Determines if participants can join the session later.

## BreakoutSession

Contains information for a specific breakout session.

### 1. getName(): String

The name of the breakout session.

### 2. getSessionId(): String

The unique session ID of the breakout session.

### 3. isAssigned(): Boolean

Indicates if the session is assigned by the host or co-host.

## Attendee Support Methods

This section describes attendee support methods.

### Join/Leave Breakout Session

Join a breakout session.

```kotlin
webex.phone.call.joinBreakoutSession(breakoutSession: BreakoutSession)
```

Return to the main session.

```kotlin
webex.phone.call.returnToMainSession()
```

## Breakout Session Events



> **Info**
>
> To receive breakout events, developers must set a [CallObserver](https://webex.github.io/webex-android-sdk/-android--s-d-kv6--doc/com.ciscowebex.androidsdk.phone/-call-observer/index.html) using the [Call.setObserver method](https://webex.github.io/webex-android-sdk/-android--s-d-kv6--doc/com.ciscowebex.androidsdk.phone/-call/index.html#-960048030%2FFunctions%2F-57558404) and override the breakout events.



### 1. Session Enabled

Triggered when breakout sessions are enabled for a meeting.

```kotlin
webex.phone.callObserver.onSessionEnabled
```

### 2. Session Started

Occurs when a breakout session starts, returning a breakout object with session info:

```kotlin
webex.phone.callObserver.onSessionStarted(breakout: Breakout)
```

### 3. Session Joined

Occurs when an attendee joins a breakout session, either manually or when assigned and started by the host:

```kotlin
webex.phone.callObserver.onSessionJoined(breakoutSession: BreakoutSession)
```

### 4. Breakout Sessions List Updated

Triggered when the list of joinable breakout sessions for an attendee is updated:

```kotlin
webex.phone.callObserver.onJoinableSessionUpdated(breakoutSessions: List<BreakoutSession>)
```

### 5. Breakout Updated

Triggered when breakout settings are updated:

```kotlin
webex.phone.callObserver.onBreakoutUpdated(breakout: Breakout)
```

### 6. Joined Session Updated

Triggered when the breakout session an attendee has joined:

```kotlin
webex.phone.callObserver.onJoinedSessionUpdated(breakoutSession: BreakoutSession)
```

### 7. Broadcast Message Received

Occurs when a broadcast message from the host is received by the participant in a session:

```kotlin
webex.phone.callObserver.onBroadcastMessageReceivedFromHost(message: String)
```

### 8. Host Asks Participants To Return To Main Session

Triggered when the host requests participants to return to the main meeting:

```kotlin
webex.phone.callObserver.onHostAskingReturnToMainSession()
```

### 9. Session Closing

Occurs when the breakout session is about to close, either immediately or after a delay configured by the host or co-host. The delay can be retrieved using the `Breakout.getDelay()` method:

```kotlin
webex.phone.callObserver.onSessionClosing()
```

### 10. Returned to Main Session

Triggered when a participant returns to the main session:

```kotlin
webex.phone.callObserver.onReturnedToMainSession()
```

### 11. Error Occurred

Triggered when an error occurs while joining a session or returning to the main session:

```kotlin
webex.phone.callObserver.onBreakoutError(error: BreakoutSession.BreakoutSessionError)
```

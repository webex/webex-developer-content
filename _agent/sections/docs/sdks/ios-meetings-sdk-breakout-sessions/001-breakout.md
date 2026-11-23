---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Breakout
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

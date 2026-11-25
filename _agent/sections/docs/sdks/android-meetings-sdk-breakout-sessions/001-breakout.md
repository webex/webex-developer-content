---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-breakout-sessions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Breakout
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-breakout-sessions). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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

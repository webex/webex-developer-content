---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- BreakoutSession
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

## BreakoutSession

Contains information for a specific breakout session.

### 1. name: String

The name of the breakout session.

### 2. sessionId: String

The unique session ID of the breakout session.

### 3. isAssigned: Bool

Indicates if the session is assigned by the host or co-host.

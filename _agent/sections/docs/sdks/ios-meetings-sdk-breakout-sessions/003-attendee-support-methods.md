---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-breakout-sessions
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Attendee Support Methods
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

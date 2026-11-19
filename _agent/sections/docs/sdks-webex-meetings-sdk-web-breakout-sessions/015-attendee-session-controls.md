---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Attendee session controls
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Attendee session controls

### Join a session

An attendee can join an active session when its `allowed`, `assigned`, or `requested` state permits joining.

```javascript
const targetSession = meeting.breakouts.breakouts.models.find(
  (session) => session.sessionId === targetSessionId
);

if (!targetSession) {
  throw new Error('The requested breakout session is not available.');
}

await targetSession.join();
```

The `requested` property indicates that a host asked the attendee to move to that session. Refresh the UI from each update event instead of retaining a stale requested-session reference.

### Leave a session

Return from the current breakout session to the main meeting.

```javascript
if (!meeting.breakouts.isInMainSession) {
  await meeting.breakouts.currentBreakoutSession.leave();
}
```

Calling `leave()` while already in the main session throws an error. Applications should also respect `allowBackToMain` when deciding whether to display a Leave control.

### Ask for help

An attendee in a breakout session can request help from the host or cohost.

```javascript
if (meeting.breakouts.isActiveBreakout) {
  await meeting.breakouts.currentBreakoutSession.askForHelp();
}
```

Hosts and cohosts receive `meeting:breakouts:askForHelp` with the participant and session identifier. Disable repeated requests while one is pending to avoid duplicate notifications.

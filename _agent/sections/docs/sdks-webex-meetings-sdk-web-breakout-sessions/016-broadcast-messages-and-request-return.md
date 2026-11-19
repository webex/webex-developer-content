---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Broadcast messages and request return
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Broadcast messages and request return

### Broadcast to all sessions

Send a message to every active breakout session.

```javascript
await meeting.breakouts.broadcast(
  'The sessions will end in five minutes.'
);
```

Omit options to send the message without a role filter. The supported role filters are `cohosts` and `presenters`.

```javascript
await meeting.breakouts.broadcast('Host update', {
  cohosts: true,
  presenters: true,
});
```

### Broadcast to one session

Call `broadcast()` on a `Breakout` model to target one session.

```javascript
await targetSession.broadcast('Please select a presenter.');
```

Receive messages through the meeting event. Treat message text as untrusted user content and render it as text, not HTML.

```javascript
function handleBreakoutMessage(event) {
  showBreakoutMessage({
    message: event.message,
    senderUserId: event.senderUserId,
    sentTime: event.sentTime,
  });
}

meeting.on('meeting:breakouts:message', handleBreakoutMessage);
```

In the current SDK implementation, `event.sessionId` is populated from the receiver's `currentBreakoutSession`. It is not guaranteed to identify the session that originally received the broadcast, so do not use it to route or authorize a message.

### Ask everyone to return

Request that all breakout participants return to the main meeting.

```javascript
await meeting.breakouts.askAllToReturn();
```

Attendees receive `meeting:breakouts:askReturnToMain`. Their application should display the request and use `currentBreakoutSession.leave()` when the attendee returns.

```javascript
function handleAskReturnToMain() {
  showReturnToMainRequest();
}

meeting.on('meeting:breakouts:askReturnToMain', handleAskReturnToMain);
```

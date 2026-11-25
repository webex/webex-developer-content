---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Start and end breakout sessions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Start and end breakout sessions

### Start sessions

Start the configured group after initial assignments are complete.

```javascript
const assignmentBehavior = 'participant-choice';

await meeting.breakouts.start({
  id: breakoutGroup.id,
  allowBackToMain: true,
  allowToJoinLater: assignmentBehavior !== 'automatic',
});
```

When `allowToJoinLater` is `false`, the meeting service requests assigned attendees to move as sessions start. When it is `true`, attendees can join later, which is appropriate when participants choose a session.

The SDK does not display a notification. An attendee application should listen for `meeting:breakouts:update`, find a session whose `requested` or `assignedCurrent` state is true, and display an invitation or move experience. Call that session model's `join()` method when the attendee accepts or when application policy permits an immediate move.

```javascript
function handleBreakoutInvitation() {
  const requestedSession = meeting.breakouts.breakouts.models.find(
    (session) =>
      !session.isMain &&
      (session.requested || session.assignedCurrent)
  );

  if (requestedSession) {
    showBreakoutInvitation(requestedSession);
  }
}

meeting.on('meeting:breakouts:update', handleBreakoutInvitation);
```

Use these properties to check the active state:

```javascript
const inProgress = meeting.breakouts.isBreakoutInProgress();
const status = meeting.breakouts.breakoutStatus;
const localUserIsInBreakout = meeting.breakouts.isActiveBreakout;
```

### End sessions

End active sessions with the required return countdown.

```javascript
await meeting.breakouts.end({delayCloseTime: 60});
```

Use `0` for immediate closure.

```javascript
await meeting.breakouts.end({delayCloseTime: 0});
```

Listen for `meeting:breakouts:closing` to display the closing countdown. Continue listening for `meeting:breakouts:update`, and consider the workflow closed only when `isBreakoutInProgress()` returns `false`.

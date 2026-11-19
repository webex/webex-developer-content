---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Reset breakout sessions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Reset breakout sessions

Reset is an application workflow rather than a single SDK call. If sessions are active, end them and wait until the SDK reports that they are closed. Then call `clearSessions()` and reset local form, selection, and roster state.

```javascript
function waitForBreakoutsToClose(timeoutMs = 10000) {
  if (!meeting.breakouts.isBreakoutInProgress()) {
    return Promise.resolve();
  }

  return new Promise((resolve, reject) => {
    const handleUpdate = () => {
      if (!meeting.breakouts.isBreakoutInProgress()) {
        window.clearTimeout(timeoutId);
        meeting.off('meeting:breakouts:update', handleUpdate);
        resolve();
      }
    };

    const timeoutId = window.setTimeout(() => {
      meeting.off('meeting:breakouts:update', handleUpdate);
      reject(new Error('Timed out waiting for breakout sessions to close.'));
    }, timeoutMs);

    meeting.on('meeting:breakouts:update', handleUpdate);
    handleUpdate();
  });
}

if (meeting.breakouts.isBreakoutInProgress()) {
  await meeting.breakouts.end({delayCloseTime: 0});
  await waitForBreakoutsToClose();
}

await meeting.breakouts.clearSessions();
resetBreakoutUIState();
```

Do not clear the application UI before `clearSessions()` succeeds. If the service request fails, preserve the last confirmed state and provide a retry action.

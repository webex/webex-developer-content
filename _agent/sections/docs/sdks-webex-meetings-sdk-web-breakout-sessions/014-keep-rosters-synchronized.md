---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Keep rosters synchronized
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Parent context

## Manage participants

Use `assign()` for in-meeting participants, both before and after sessions start. Use `dynamicAssign()` only to admit a participant from the lobby directly into an active breakout. To move the local host or cohost client, call `join()` on the target `Breakout` model.

## Selected section

### Keep rosters synchronized

The SDK processes live breakout roster events. Request initial rosters after sessions start by calling `queryRosters()`.

```javascript
meeting.breakouts.queryRosters();
```

`queryRosters()` does not return a roster promise. Wait for `meeting:breakouts:update`, then read the current session roster from `meeting.members.membersCollection` and other session rosters from their `Breakout` models.

```javascript
function getSessionMembers(session) {
  const currentSession = meeting.breakouts.currentBreakoutSession;
  const membersCollection = currentSession?.sessionId === session.sessionId
    ? meeting.members.membersCollection
    : session.members?.membersCollection;

  return Object.values(membersCollection?.getAll?.() || {});
}

function refreshBreakoutRosters() {
  const sessions = [...meeting.breakouts.breakouts.models];
  const currentSession = meeting.breakouts.currentBreakoutSession;

  if (
    currentSession?.sessionId &&
    !sessions.some((session) => session.sessionId === currentSession.sessionId)
  ) {
    sessions.push(currentSession);
  }

  sessions.forEach((session) => {
    renderSessionParticipants(session, getSessionMembers(session));
  });

  refreshUnassignedParticipants();
}

meeting.on('meeting:breakouts:update', refreshBreakoutRosters);
meeting.members.on('members:update', refreshBreakoutRosters);
```

Scheduled meetings can contain preassignments. The SDK stores them in `meeting.breakouts.preAssignments` and emits `meeting:breakouts:preAssignmentsUpdate` when they are loaded or changed.

```javascript
function handlePreAssignmentsUpdate() {
  renderPreAssignments(meeting.breakouts.preAssignments);
}

meeting.on(
  'meeting:breakouts:preAssignmentsUpdate',
  handlePreAssignmentsUpdate
);

meeting.breakouts.queryPreAssignments();
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Before you begin

Enable breakout capability when joining the meeting. This capability cannot be added after the join request has completed.

```javascript
await meeting.join({
  breakoutsSupported: true,
});
```

For the complete join flow, see [Join a Meeting](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting).

Register listeners before starting the breakout workflow. The `meeting:breakouts:update` event is the primary signal to read the latest session and roster state.

```javascript
function refreshBreakoutUI() {
  const sessions = meeting.breakouts.breakouts.models;
  const currentSession = meeting.breakouts.currentBreakoutSession;

  renderBreakoutSessions({sessions, currentSession});
}

meeting.on('meeting:breakouts:update', refreshBreakoutUI);
```

The update event does not provide a state snapshot. Always read current state from `meeting.breakouts` in the listener.

Only hosts and cohosts can configure or manage breakout sessions. Check the permission before displaying or running management controls.

```javascript
if (!meeting.breakouts.canManageBreakouts) {
  throw new Error('Only a host or cohost can manage breakout sessions.');
}
```



> **Info**
>
> Breakout availability also depends on the meeting configuration and the local user's role. The SDK provides state and methods but does not render breakout dialogs, notifications, or participant tables.

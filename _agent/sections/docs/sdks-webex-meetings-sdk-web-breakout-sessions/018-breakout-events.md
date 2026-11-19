---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Breakout events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Breakout events

Register these events on the `Meeting` object with `meeting.on()`.

| Event | Payload | Description |
| --- | --- | --- |
| `meeting:breakouts:update` | None | Breakout configuration, local assignment state, or roster information changed. Read the latest state from `meeting.breakouts`. |
| `meeting:breakouts:closing` | None | Active breakout sessions entered the closing state. |
| `meeting:breakouts:message` | `{senderUserId, sentTime, message, sessionId}` | A breakout broadcast message was received. `sessionId` reflects the receiver's current session and is not guaranteed to identify the broadcast target. |
| `meeting:breakouts:askReturnToMain` | None | The host or cohost requested that attendees return to the main meeting. |
| `meeting:breakouts:leave` | None | The local user moved from a breakout session to the main meeting. |
| `meeting:breakouts:askForHelp` | `{participant, sessionId}` | A participant requested help from the host or cohost. |
| `meeting:breakouts:preAssignmentsUpdate` | None | Scheduled breakout preassignment data was loaded or changed. Read it from `meeting.breakouts.preAssignments`. |

Remove listeners when the meeting view is destroyed to prevent duplicate handlers.

```javascript
meeting.off('meeting:breakouts:update', refreshBreakoutUI);
meeting.off('meeting:breakouts:update', handleBreakoutInvitation);
meeting.off('meeting:breakouts:update', refreshBreakoutRosters);
meeting.members.off('members:update', refreshBreakoutRosters);
meeting.off(
  'meeting:breakouts:preAssignmentsUpdate',
  handlePreAssignmentsUpdate
);
meeting.off('meeting:breakouts:message', handleBreakoutMessage);
meeting.off('meeting:breakouts:askReturnToMain', handleAskReturnToMain);
```

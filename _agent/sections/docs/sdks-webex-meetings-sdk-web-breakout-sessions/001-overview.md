---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Overview

Breakout sessions divide a meeting into smaller groups with separate participant rosters. The `meeting.breakouts` object provides host and cohost controls for configuring and managing sessions, and attendee controls for joining, leaving, and interacting with a session.

The SDK exposes two related objects:

- `meeting.breakouts` is the `Breakouts` controller for the meeting.
- Each model in `meeting.breakouts.breakouts.models` is a `Breakout` session known to the current user.

The current joined session is available separately as `meeting.breakouts.currentBreakoutSession`. It is not a member of the `meeting.breakouts.breakouts` collection.

```javascript
const breakouts = meeting.breakouts;
const availableSessions = breakouts.breakouts.models;
const currentSession = breakouts.currentBreakoutSession;
```

The following controller properties are useful when building a breakout user interface:

| Property | Description |
| --- | --- |
| `allowBackToMain` | Whether the current attendee can return to the main meeting. |
| `breakoutGroupId` | Identifier of the active breakout group. |
| `breakoutStatus` | Current group status, such as `PENDING`, `OPEN`, `CLOSING`, or `CLOSED`. |
| `canManageBreakouts` | Whether the current user can use host and cohost management controls. |
| `currentBreakoutSession` | Session currently joined by the local user. |
| `delayCloseTime` | Closing countdown, in seconds. |
| `enableBreakoutSession` | Whether breakout sessions are enabled for the meeting. |
| `isActiveBreakout` | Whether the local user is in an open or closing breakout session. |
| `isInMainSession` | Whether the local user is in the main meeting. |
| `mainGroupId` | Identifier of the main meeting group. |
| `mainSessionId` | Identifier of the main meeting session. |
| `preAssignments` | Scheduled breakout preassignment data, when available. |

Each `Breakout` session model includes the following state:

| Property | Type | Description |
| --- | --- | --- |
| `sessionId` | String | Unique identifier for the session model. |
| `groupId` | String | Identifier of the group containing the session. |
| `name` | String | Display name of the session. |
| `sessionType` | String | `MAIN` for the main meeting or `BREAKOUT` for a breakout session. |
| `isMain` | Boolean | Whether the model represents the main meeting. |
| `active` | Boolean | Whether the session is active. |
| `allowed` | Boolean | Whether the local user is allowed to join the session. |
| `assigned` | Boolean | Whether the local user is assigned to the session. |
| `assignedCurrent` | Boolean | Whether the local user is assigned and currently expected in the session. |
| `requested` | Boolean | Whether the host requested that the local user move to the session. |
| `current` | Boolean | Whether this is the local user's joined session. |
| `members` | Object | Roster for a session the local user has not joined. Members are in `members.membersCollection`. |

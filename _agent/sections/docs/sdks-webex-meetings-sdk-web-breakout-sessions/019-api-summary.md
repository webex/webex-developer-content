---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- API summary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## API summary

The following `Breakouts` methods are implemented in the current SDK source.

| Method | Description |
| --- | --- |
| `toggleBreakout(enable)` | Enables or disables breakout sessions for the meeting. |
| `create(params)` | Creates a breakout group and its pending sessions. |
| `clearSessions()` | Deletes the breakout session configuration. |
| `start(params)` | Starts the configured breakout group. |
| `end(params)` | Ends active sessions, optionally with a closing delay. |
| `getBreakout(editlock)` | Retrieves the configuration and optionally obtains an edit lock. |
| `update(params, unlockEdit)` | Updates a group or session and optionally releases the edit lock. |
| `enableAndLockBreakout()` | Ensures the breakout resource exists and begins the edit-lock flow. |
| `lockBreakout()` | Obtains or keeps alive an edit lock. |
| `hasBreakoutLocked()` | Indicates whether this client holds the edit lock. |
| `unLockEditBreakout()` | Releases a retained edit lock. |
| `assign(sessions)` | Updates participant ID and email assignments before or after sessions start. Send the complete assignment state for every session. |
| `dynamicAssign(sessions)` | Admits lobby participants directly into an active breakout session. |
| `removeFromBreakout(participants)` | Returns unassigned participants who independently joined through **Let anyone join** to the main meeting. |
| `moveToLobby(sessions)` | Moves participants to the main meeting lobby. |
| `broadcast(message, options)` | Sends a message to all breakout sessions. |
| `askAllToReturn()` | Requests that all attendees return to the main meeting. |
| `queryRosters()` | Requests breakout rosters; results arrive through update events. |
| `queryPreAssignments()` | Requests scheduled breakout preassignments; results arrive through an event. |
| `isBreakoutInProgress()` | Indicates whether the breakout group is open or closing. |
| `getMainSession()` | Returns the main-session `Breakout` model. |

The following methods are available on a `Breakout` session model.

| Method | Description |
| --- | --- |
| `join()` | Moves the local user to that session. |
| `leave()` | Returns the local user from a breakout session to the main meeting. |
| `askForHelp()` | Sends a help request to the host or cohost. |
| `broadcast(message, options)` | Sends a message to that session. |

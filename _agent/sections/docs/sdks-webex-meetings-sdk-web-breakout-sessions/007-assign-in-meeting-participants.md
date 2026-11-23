---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Assign in-meeting participants
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

### Assign in-meeting participants

The [move helper below](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions#move-participants-into-a-session) uses `updateBreakoutAssignments()` to pass the complete array of session assignments to `assign()`, preserving other sessions and their confirmed settings. Each session entry contains the following fields, both before and after sessions start.

| Property | Type | Description |
| --- | --- | --- |
| `id` | String | Target session identifier from the service configuration. |
| `memberIds` | Array | Meeting participant IDs assigned to the session. |
| `emails` | Array | Invitee email addresses assigned to the session. |
| `anyone` | Boolean | Whether unassigned participants can join the session. |

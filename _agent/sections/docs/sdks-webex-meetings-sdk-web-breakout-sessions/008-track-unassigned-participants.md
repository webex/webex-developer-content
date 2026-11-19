---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Track unassigned participants
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

### Track unassigned participants

The SDK does not maintain a separate unassigned collection. Build it in application state by comparing eligible meeting and lobby participants with the IDs assigned to or present in the session rosters. Recalculate this state after every breakout or meeting roster update, including after a remove operation.

Keep meeting and lobby participants in separate presentation groups if your UI distinguishes them. Include a participant only once. Use a meeting participant's SDK ID for assignment actions, and retain email-based preassignments when building the complete payload. Compare both IDs and verified email identities before classifying a participant as unassigned. If their email identity is unresolved, show that state and disable assignment changes for that participant.

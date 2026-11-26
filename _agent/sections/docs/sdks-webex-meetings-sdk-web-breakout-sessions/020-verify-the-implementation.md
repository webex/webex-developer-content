---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the implementation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Verify the implementation

Use the [Browser Meetings Sample](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/) to exercise the breakout APIs visually. Enable **Support breakout sessions** before joining, then use the **Breakout Sessions** controls as a host or cohost.

Verify the following scenarios with at least one host and one attendee:

1. Join every test client with `breakoutsSupported: true`.
2. Confirm that only a host or cohost sees management controls.
3. Create the requested number of sessions for automatic, manual, and participant-choice assignment modes.
4. Start sessions and confirm that assigned attendees receive update state that the application presents as a join or move notification.
5. Confirm that participant moves, exchanges, removal, lobby movement, and host joins update both session and unassigned rosters after the next event.
6. Rename a pending session and toggle `anyoneCanJoin` while holding the edit lock.
7. Broadcast to all sessions and one session, request return, end the sessions, and reset the configuration.

Also verify these assignment cases:

- In-meeting moves and exchanges use `assign()` before and after sessions start. Lobby-to-breakout admission uses `dynamicAssign()` only while sessions are active.
- Automatic assignment includes only eligible in-meeting members, uses their verified identities, and preserves other assignments and session settings from the locked snapshot. Lobby members stay separate until admitted into an active breakout.
- Moving or exchanging an attendee who has both an SDK ID and an email preassignment retains both at the destination. Unrelated assignments and each session's **Let anyone join** setting remain unchanged, including an explicitly disabled setting.
- Removing an assigned or email-preassigned attendee uses `assign()` and clears the matching ID and email. Removing an unassigned attendee who joined independently uses `removeFromBreakout()`.
- A roster member without a verified `assignmentEmails` mapping cannot be moved, exchanged, removed, or classified as definitely unassigned. Missing configuration or an unavailable `anyoneCanJoin` setting also blocks assignment changes without overwriting existing state.
- An exchange rejects stale source selections, duplicate participants, and identities assigned across multiple sessions before changing either assignment.
- A second settings edit, automatic assignment, move, exchange, or removal cannot run while another edit is pending or a local lock remains. Settings updates reject missing lock tokens and stale session selections. After a failed request, the error is shown and the user can retry from refreshed state.
- With two host or cohost clients, an assignment edit must acquire the service lock before reading its snapshot. A competing editor must wait or retry from a fresh locked snapshot. Verify lock denial, lock loss, and pending release without falling back to an unlocked `assign()` call.

Important failure cases include missing breakout capability at join, insufficient host or cohost permission, an edit lock held by another client, a stale participant or session ID, a roster update that has not arrived yet, and an attempt to add a session after breakouts have started. Surface a clear action to the user, retain the last confirmed SDK state, and avoid logging access tokens or complete service responses.

For the complete SDK reference, see the [Webex JavaScript SDK API documentation](https://webex.github.io/webex-js-sdk/api/).

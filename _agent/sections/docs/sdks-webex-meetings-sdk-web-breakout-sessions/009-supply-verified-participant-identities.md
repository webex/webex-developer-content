---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Supply verified participant identities
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

### Supply verified participant identities

The SDK's roster `Member` does not expose `email`, `emailAddress`, or a top-level `person.email`. The helpers below instead require application-owned participant inputs containing `id` and `assignmentEmails`. Populate `assignmentEmails` from verified application invite or preassignment records linked to the current roster member. For a resolvable Webex person, the SDK also documents looking up `webex.people.get(member.participant.identity)` and reading the returned person's `emails`; this requires the People plugin and authorized access. Use the person's identity for that lookup, not the meeting member ID.

Verify that the email list includes the aliases used by the participant's preassignments. Guests, missing identity data, unavailable permissions, or incomplete profile aliases may require your application's own verified records. A failed or incomplete lookup is an unknown mapping, not an empty email list. Rebuild these inputs when the meeting or the participant's roster identity changes.

Use `assignmentEmails: []` only when your application has confirmed that the participant has no email-based identity to match. Omit the field while the mapping is unresolved; the helpers reject that input before either assignment or removal. Do not infer identity from a display name.

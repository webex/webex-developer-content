---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Remove participants from breakouts
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

### Remove participants from breakouts

For a participant assigned by SDK ID or preassigned by email, remove the participant from the complete assignment state and call `assign()`. Use `removeFromBreakout()` only when the participant was not assigned but independently joined a session through **Let anyone join**.

```javascript
async function removeParticipantFromBreakout(participant) {
  await updateBreakoutAssignments(async (assignments) => {
    if (isParticipantAssigned(assignments, participant)) {
      removeParticipantFromAssignments(assignments, participant);
      return;
    }

    if (!participant.id) {
      throw new Error('The participant does not have an SDK ID.');
    }

    await meeting.breakouts.removeFromBreakout([participant.id]);
    return false;
  });
}
```

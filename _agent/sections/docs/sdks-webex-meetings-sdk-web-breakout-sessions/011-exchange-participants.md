---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Exchange participants
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

### Exchange participants

Exchange two in-meeting participants assigned to different sessions by updating both destinations and calling `assign()` once. Validate both source assignments against the locked configuration before changing either one.

```javascript
async function exchangeParticipants(
  firstSessionId,
  firstParticipant,
  secondSessionId,
  secondParticipant
) {
  if (
    !firstSessionId ||
    !secondSessionId ||
    firstSessionId === secondSessionId ||
    !firstParticipant ||
    !secondParticipant
  ) {
    throw new Error('Select participants from two different sessions.');
  }

  const firstIdentityEmails = new Set(
    getParticipantEmails(firstParticipant).map((email) => email.toLowerCase())
  );
  const hasSharedEmail = getParticipantEmails(secondParticipant).some(
    (email) => firstIdentityEmails.has(email.toLowerCase())
  );

  if (
    (firstParticipant.id && firstParticipant.id === secondParticipant.id) ||
    hasSharedEmail
  ) {
    throw new Error('Select two distinct participants with unambiguous identities.');
  }

  await updateBreakoutAssignments((assignments) => {
    const firstAssignment = assignments.find(({id}) => id === firstSessionId);
    const secondAssignment = assignments.find(({id}) => id === secondSessionId);

    if (!firstAssignment || !secondAssignment) {
      throw new Error('A source or target assignment is unavailable.');
    }

    const firstSources = assignments.filter(
      (assignment) => isParticipantAssigned([assignment], firstParticipant)
    );
    const secondSources = assignments.filter(
      (assignment) => isParticipantAssigned([assignment], secondParticipant)
    );

    if (
      firstSources.length !== 1 || firstSources[0] !== firstAssignment ||
      secondSources.length !== 1 || secondSources[0] !== secondAssignment
    ) {
      throw new Error('Assignments changed or are ambiguous. Refresh and select again.');
    }

    const firstEmails = removeParticipantFromAssignments(assignments, firstParticipant);
    const secondEmails = removeParticipantFromAssignments(assignments, secondParticipant);
    addParticipantToAssignment(firstAssignment, secondParticipant, secondEmails);
    addParticipantToAssignment(secondAssignment, firstParticipant, firstEmails);
  });
}
```

When several participants are present, the application must identify two distinct participants and their source sessions. Disable exchange until both selections are valid. The helper rejects stale selections and identities assigned across multiple sessions before sending an update.

These checks validate configured assignments, not physical roster presence. An attendee who independently joined through **Let anyone join** may have no source assignment. Use the move flow above to assign that attendee to a selected destination; an application offering roster-based exchanges must also validate current roster selections separately.

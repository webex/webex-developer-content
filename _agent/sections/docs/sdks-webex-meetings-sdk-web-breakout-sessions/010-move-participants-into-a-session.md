---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Move participants into a session
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

### Move participants into a session

For in-meeting participants, remove each participant from any current assignment, add them to the target assignment, and call `assign()` once with the complete updated state.

```javascript
function getParticipantEmails(participant) {
  const emails = participant?.assignmentEmails;

  if (!Array.isArray(emails)) {
    throw new Error('Resolve the participant email mapping before changing assignments.');
  }

  if (emails.some((email) => typeof email !== 'string' || !email.trim())) {
    throw new Error('The participant email mapping contains an invalid address.');
  }

  return [...new Set(emails.map((email) => email.trim()))];
}

function isParticipantAssigned(assignments, participant) {
  const participantEmails = new Set(
    getParticipantEmails(participant).map((email) => email.toLowerCase())
  );

  return assignments.some((assignment) =>
    assignment.memberIds.includes(participant.id) ||
    assignment.emails.some(
      (email) => participantEmails.has(email.toLowerCase())
    )
  );
}

function removeParticipantFromAssignments(assignments, participant) {
  const participantEmails = new Set(
    getParticipantEmails(participant).map((email) => email.toLowerCase())
  );
  const retainedEmails = [];

  assignments.forEach((assignment) => {
    assignment.memberIds = assignment.memberIds.filter(
      (memberId) => memberId !== participant.id
    );
    assignment.emails = assignment.emails.filter((email) => {
      if (participantEmails.has(email.toLowerCase())) {
        retainedEmails.push(email);
        return false;
      }

      return true;
    });
  });

  return [...new Set(retainedEmails)];
}

function addParticipantToAssignment(assignment, participant, retainedEmails = []) {
  if (participant.id) {
    assignment.memberIds = [
      ...new Set([...assignment.memberIds, participant.id]),
    ];
  }

  let emails = retainedEmails;

  if (!participant.id && !emails.length) {
    const [participantEmail] = getParticipantEmails(participant);

    if (!participantEmail) {
      throw new Error('The participant does not have an SDK ID or email.');
    }

    emails = [participantEmail];
  }

  assignment.emails = [
    ...new Set([...assignment.emails, ...emails]),
  ];
}

async function moveMeetingParticipants(targetSessionId, participants) {
  if (!targetSessionId || !Array.isArray(participants) || !participants.length) {
    throw new Error('Select a target session and at least one participant.');
  }

  await updateBreakoutAssignments((assignments) => {
    const targetAssignment = assignments.find(
      ({id}) => id === targetSessionId
    );

    if (!targetAssignment) {
      throw new Error('The target breakout assignment is unavailable.');
    }

    participants.forEach((participant) => {
      const retainedEmails = removeParticipantFromAssignments(assignments, participant);
      addParticipantToAssignment(targetAssignment, participant, retainedEmails);
    });
  });
}
```

For an attendee with both an SDK ID and an existing email preassignment, these helpers move both to the destination. They preserve the stored email spelling and do not create a new email preassignment for an attendee who was assigned only by ID.

After verifying the roster-member-to-email association, pass an enriched participant input to move, exchange, or removal actions. For example:

```javascript
const participant = {
  id: 'participant-id',
  assignmentEmails: ['invitee@example.com'],
};

await moveMeetingParticipants(targetSessionId, [participant]);
```

For a lobby participant, use `dynamicAssign()` only after the breakout group is active. This admits the participant directly from the lobby into the target breakout.

```javascript
const lobbyParticipantIds = lobbyParticipants.map(
  (participant) => participant.id
);

if (
  !targetSessionId ||
  !lobbyParticipantIds.length ||
  lobbyParticipantIds.some((participantId) => !participantId)
) {
  throw new Error('Select a target session and valid lobby participants.');
}

await meeting.breakouts.dynamicAssign([
  {
    id: targetSessionId,
    participants: lobbyParticipantIds,
    targetState: 'JOINED',
  },
]);
```

For the local host or cohost client, find the target `Breakout` model and call `join()`.

```javascript
const targetSession = meeting.breakouts.breakouts.models.find(
  (session) => session.sessionId === targetSessionId
);

if (!targetSession) {
  throw new Error('The target breakout session is unavailable.');
}

await targetSession.join();
```

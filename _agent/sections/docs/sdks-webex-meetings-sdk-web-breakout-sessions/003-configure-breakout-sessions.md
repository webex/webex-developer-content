---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure breakout sessions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

## Configure breakout sessions

The host or cohost enables the breakout resource, creates every required session, applies any initial assignments, and starts the group.

### Enable breakout sessions

Use `toggleBreakout()` to enable or disable breakout sessions for the meeting.

```javascript
await meeting.breakouts.toggleBreakout(true);
```

To disable breakout sessions later, pass `false`.

```javascript
await meeting.breakouts.toggleBreakout(false);
```

### Create sessions

Create all required sessions before starting the group. Each session requires a name and can optionally allow unassigned participants to join.

```javascript
function getBreakoutSessionId(session) {
  return session?.sessionId || session?.id;
}

const requestedSessionCount = 3;
const sessions = Array.from({length: requestedSessionCount}, (_, index) => ({
  name: `Breakout session ${index + 1}`,
  anyoneCanJoin: false,
}));

const createResult = await meeting.breakouts.create({
  allowBackToMain: true,
  allowToJoinLater: false,
  delayCloseTime: 60,
  sessions,
});

let breakoutGroup = createResult?.body?.groups?.[0];

if (
  !breakoutGroup?.id ||
  !breakoutGroup.sessions?.length ||
  breakoutGroup.sessions.some((session) => !getBreakoutSessionId(session))
) {
  const currentConfiguration = await meeting.breakouts.getBreakout(false);
  breakoutGroup = currentConfiguration?.body?.groups?.find(
    (group) =>
      group.id &&
      group.status !== 'CLOSED' &&
      group.sessions?.length &&
      group.sessions.every((session) => getBreakoutSessionId(session))
  );
}

if (!breakoutGroup?.id || !breakoutGroup.sessions?.length) {
  throw new Error('The breakout session configuration is not available yet.');
}
```

| Parameter | Type | Description |
| --- | --- | --- |
| `sessions` | Array | Session definitions. Each definition contains `name` and `anyoneCanJoin`. |
| `allowBackToMain` | Boolean | Whether attendees can return to the main meeting. |
| `allowToJoinLater` | Boolean | Whether assigned attendees can join later instead of being requested to move immediately. |
| `delayCloseTime` | Number | Seconds allowed for attendees to return when sessions close. Use `0` for immediate closure. |

The service response uses `id` for group and session identifiers. After the SDK builds a `Breakout` model, use its `groupId` and `sessionId` properties.

### Choose an assignment behavior

The SDK does not accept an assignment-mode value such as `automatic`, `manual`, or `choose`. These choices are application behavior implemented with the SDK methods and payloads below.

| Application choice | SDK behavior |
| --- | --- |
| Assign participants automatically | Distribute eligible IDs in application code, call `assign()` before start, and normally start with `allowToJoinLater: false`. |
| Assign participants manually | Do not call `assign()` initially. Keep participants in an unassigned list and call `assign()` when the host assigns in-meeting participants, before or after start. Use `dynamicAssign()` only to admit lobby participants directly into an active breakout. |
| Let participants choose any session | Create sessions with `anyoneCanJoin: true` and start with `allowToJoinLater: true`. |

For automatic assignment, filter the meeting roster according to your application rules and distribute participants across the current sessions. Define the [shared assignment helpers](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions#build-the-current-assignment-payload) and [verified participant inputs](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions#supply-verified-participant-identities) below before calling this function. Supply an input for every eligible roster member. This example excludes the local user, host, devices, lobby participants, participants no longer in the meeting, and clients without confirmed breakout support.

```javascript
async function assignMeetingParticipantsAutomatically(participantInputs) {
  if (!Array.isArray(participantInputs)) {
    throw new Error('Supply verified participant inputs for automatic assignment.');
  }

  const inputsById = new Map(participantInputs.map((participant) => [
    participant.id, participant,
  ]));
  const meetingMembers = Object.values(meeting.members.membersCollection.getAll());
  const eligibleMembers = meetingMembers.filter((member) =>
    member.id &&
    !member.isSelf &&
    !member.isHost &&
    !member.isDevice &&
    member.isInMeeting === true &&
    member.supportsBreakouts === true
  );
  const participants = eligibleMembers.map((member) => inputsById.get(member.id));

  if (participants.some((participant) => !participant)) {
    throw new Error('Resolve every eligible participant identity before assigning.');
  }

  if (!participants.length) {
    return;
  }

  await updateBreakoutAssignments((assignments) => {
    participants.forEach((participant, index) => {
      const retainedEmails = removeParticipantFromAssignments(assignments, participant);
      addParticipantToAssignment(
        assignments[index % assignments.length], participant, retainedEmails
      );
    });
  });
}
```

Options such as assigning cohosts automatically belong in the application's eligibility filter. Automatic assignment preserves unrelated IDs, email preassignments, and each session's confirmed **Let anyone join** setting through the complete-state helper. If the user selects manual assignment, omit the automatic assignment call and keep eligible meeting and lobby participants in separate unassigned presentation groups. In-meeting participants can be assigned before or after the sessions start. Lobby participants can be admitted directly only after the sessions are active, using `dynamicAssign()`.

For participant choice, set `anyoneCanJoin` on every session definition.

```javascript
const sessions = [
  {name: 'Breakout session 1', anyoneCanJoin: true},
  {name: 'Breakout session 2', anyoneCanJoin: true},
];

const createResult = await meeting.breakouts.create({sessions});
let breakoutGroup = createResult?.body?.groups?.[0];

if (
  !breakoutGroup?.id ||
  !breakoutGroup.sessions?.length ||
  breakoutGroup.sessions.some((session) => !getBreakoutSessionId(session))
) {
  const currentConfiguration = await meeting.breakouts.getBreakout(false);
  breakoutGroup = currentConfiguration?.body?.groups?.find(
    (group) =>
      group.id &&
      group.status !== 'CLOSED' &&
      group.sessions?.length &&
      group.sessions.every((session) => getBreakoutSessionId(session))
  );
}

if (!breakoutGroup?.id || !breakoutGroup.sessions?.length) {
  throw new Error('The breakout session configuration is not available yet.');
}
```

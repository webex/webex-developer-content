---
type: Guide
title: Web Meetings SDK | Breakout Sessions
display_title: Breakout Sessions
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions)

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

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

## Before you begin

Enable breakout capability when joining the meeting. This capability cannot be added after the join request has completed.

```javascript
await meeting.join({
  breakoutsSupported: true,
});
```

For the complete join flow, see [Join a Meeting](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting).

Register listeners before starting the breakout workflow. The `meeting:breakouts:update` event is the primary signal to read the latest session and roster state.

```javascript
function refreshBreakoutUI() {
  const sessions = meeting.breakouts.breakouts.models;
  const currentSession = meeting.breakouts.currentBreakoutSession;

  renderBreakoutSessions({sessions, currentSession});
}

meeting.on('meeting:breakouts:update', refreshBreakoutUI);
```

The update event does not provide a state snapshot. Always read current state from `meeting.breakouts` in the listener.

Only hosts and cohosts can configure or manage breakout sessions. Check the permission before displaying or running management controls.

```javascript
if (!meeting.breakouts.canManageBreakouts) {
  throw new Error('Only a host or cohost can manage breakout sessions.');
}
```



> **Info**
>
> Breakout availability also depends on the meeting configuration and the local user's role. The SDK provides state and methods but does not render breakout dialogs, notifications, or participant tables.



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

For automatic assignment, filter the meeting roster according to your application rules and distribute participants across the current sessions. Define the [shared assignment helpers](#build-the-current-assignment-payload) and [verified participant inputs](#supply-verified-participant-identities) below before calling this function. Supply an input for every eligible roster member. This example excludes the local user, host, devices, lobby participants, participants no longer in the meeting, and clients without confirmed breakout support.

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

## Start and end breakout sessions

### Start sessions

Start the configured group after initial assignments are complete.

```javascript
const assignmentBehavior = 'participant-choice';

await meeting.breakouts.start({
  id: breakoutGroup.id,
  allowBackToMain: true,
  allowToJoinLater: assignmentBehavior !== 'automatic',
});
```

When `allowToJoinLater` is `false`, the meeting service requests assigned attendees to move as sessions start. When it is `true`, attendees can join later, which is appropriate when participants choose a session.

The SDK does not display a notification. An attendee application should listen for `meeting:breakouts:update`, find a session whose `requested` or `assignedCurrent` state is true, and display an invitation or move experience. Call that session model's `join()` method when the attendee accepts or when application policy permits an immediate move.

```javascript
function handleBreakoutInvitation() {
  const requestedSession = meeting.breakouts.breakouts.models.find(
    (session) =>
      !session.isMain &&
      (session.requested || session.assignedCurrent)
  );

  if (requestedSession) {
    showBreakoutInvitation(requestedSession);
  }
}

meeting.on('meeting:breakouts:update', handleBreakoutInvitation);
```

Use these properties to check the active state:

```javascript
const inProgress = meeting.breakouts.isBreakoutInProgress();
const status = meeting.breakouts.breakoutStatus;
const localUserIsInBreakout = meeting.breakouts.isActiveBreakout;
```

### End sessions

End active sessions with the required return countdown.

```javascript
await meeting.breakouts.end({delayCloseTime: 60});
```

Use `0` for immediate closure.

```javascript
await meeting.breakouts.end({delayCloseTime: 0});
```

Listen for `meeting:breakouts:closing` to display the closing countdown. Continue listening for `meeting:breakouts:update`, and consider the workflow closed only when `isBreakoutInProgress()` returns `false`.

## Update session settings

Configuration and assignment updates share one edit-lock lifecycle per meeting. Define these helpers once and route settings edits and assignment actions through them. The runner obtains a fresh locked configuration, validates its token, and prevents overlapping local edits. Each callback rechecks ownership immediately before its write.

```javascript
function getBreakoutSessions(configuration) {
  const groups = configuration?.body?.groups;
  const groupId = meeting.breakouts.breakoutGroupId;

  if (!Array.isArray(groups) || typeof groupId !== 'string' || !groupId) {
    throw new Error('Refresh the breakout configuration before editing sessions.');
  }

  const currentGroup = groups.find(
    (group) => group?.id === groupId
  );

  if (!Array.isArray(currentGroup?.sessions) || !currentGroup.sessions.length) {
    throw new Error('The current breakout sessions are unavailable.');
  }

  return currentGroup.sessions;
}

function requireBreakoutEditLock(token) {
  if (
    typeof token !== 'string' ||
    !token ||
    !meeting.breakouts.hasBreakoutLocked() ||
    meeting.breakouts.editLock?.token !== token
  ) {
    throw new Error('The breakout edit lock is unavailable or was lost.');
  }
}

let breakoutEditInProgress = false;

async function withBreakoutEditLock(editConfiguration) {
  if (breakoutEditInProgress) {
    throw new Error('Wait for the current breakout edit to finish.');
  }

  if (meeting.breakouts.editLock?.token) {
    throw new Error('Wait for the current breakout edit lock to be released.');
  }

  breakoutEditInProgress = true;
  let editLockToken;

  try {
    const configuration = await meeting.breakouts.getBreakout(true);
    editLockToken = configuration?.body?.editlock?.token;

    if (configuration?.body?.editlock?.state !== 'LOCKED') {
      throw new Error('The breakout edit lock was not acquired.');
    }

    const requireOwnedLock = () => requireBreakoutEditLock(editLockToken);
    requireOwnedLock();
    await editConfiguration(configuration, requireOwnedLock);
    await meeting.breakouts.getBreakout(false);
  } finally {
    try {
      if (
        typeof editLockToken === 'string' &&
        editLockToken &&
        meeting.breakouts.editLock?.token === editLockToken
      ) {
        meeting.breakouts.unLockEditBreakout();
      }
    } finally {
      breakoutEditInProgress = false;
    }
  }
}

async function updateBreakoutSession(session, changes) {
  await withBreakoutEditLock((configuration, requireOwnedLock) => {
    const sessions = getBreakoutSessions(configuration);
    const groupId = meeting.breakouts.breakoutGroupId;

    if (
      !session?.sessionId ||
      (session?.groupId && session.groupId !== groupId) ||
      !sessions.some((item) => getBreakoutSessionId(item) === session?.sessionId)
    ) {
      throw new Error('The selected breakout session is unavailable.');
    }

    requireOwnedLock();
    return meeting.breakouts.update({
      id: groupId,
      sessions: [{id: session.sessionId, ...changes}],
    }, false);
  });
}
```

`updateBreakoutSession()` checks the selected session against the returned configuration and includes the group ID in `update()`. Passing `false` as the second argument retains the token until the shared runner refreshes state and requests release in `finally`. Keep controls disabled while an edit is pending or a local token remains; the release behavior is described in [Build the current assignment payload](#build-the-current-assignment-payload).

### Rename a session

```javascript
async function renameBreakoutSession(session, name) {
  if (typeof name !== 'string' || !name.trim()) {
    throw new Error('Enter a session name.');
  }

  await updateBreakoutSession(session, {name: name.trim()});
}
```

Call this function when the user saves a valid name or the input loses focus. It acquires its own lock through the shared runner; keep save controls disabled while another edit is pending or its token remains.

### Let anyone join

Use the same edit-lock lifecycle to update `anyoneCanJoin`.

```javascript
async function setAnyoneCanJoin(session, anyoneCanJoin) {
  if (typeof anyoneCanJoin !== 'boolean') {
    throw new Error('Choose a boolean Let anyone join setting.');
  }

  await updateBreakoutSession(session, {anyoneCanJoin});
}
```

### Add a session before creation

Add new session definitions in application state before calling `create()`.

```javascript
const sessionDefinitions = [
  {name: 'Breakout session 1', anyoneCanJoin: false},
];

sessionDefinitions.push({
  name: `Breakout session ${sessionDefinitions.length + 1}`,
  anyoneCanJoin: false,
});

await meeting.breakouts.create({
  sessions: sessionDefinitions,
});
```



> **Create sessions before start**
>
> The breakout service rejects attempts to create or add sessions after the group has started. Build the complete session list before calling `create()`, or end and clear the current configuration before creating another group.



If an update fails because another editor holds the lock, do not overwrite their configuration. Refresh the configuration, reacquire the lock, and ask the user to retry.

## Manage participants

Use `assign()` for in-meeting participants, both before and after sessions start. Use `dynamicAssign()` only to admit a participant from the lobby directly into an active breakout. To move the local host or cohost client, call `join()` on the target `Breakout` model.

### Build the current assignment payload

An `assign()` update should include the complete current assignment for every session. Obtain the service edit lock and a fresh configuration together with `getBreakout(true)`, validate the returned lock, group, and sessions, preserve assigned member IDs, preassigned email addresses, and `anyoneCanJoin`, make the required changes, and call `assign()` once while retaining that lock.

```javascript
function getAssignedMemberIds(session) {
  if (!Array.isArray(session?.assigned)) {
    return [];
  }

  return [...new Set(
    session.assigned
      .map((participant) => typeof participant === 'string'
        ? participant
        : participant?.id || participant?.memberId)
      .filter(Boolean)
  )];
}

function getAssignedEmails(session) {
  if (!Array.isArray(session?.assignedEmails)) {
    return [];
  }

  return [...new Set(
    session.assignedEmails.filter((email) => typeof email === 'string' && email)
  )];
}

function getAnyoneCanJoin(session) {
  if (typeof session?.anyoneCanJoin !== 'boolean') {
    throw new Error('The confirmed Let anyone join setting is unavailable.');
  }

  return session.anyoneCanJoin;
}

function createAssignmentState(configuration) {
  return getBreakoutSessions(configuration).map((session) => ({
    id: getBreakoutSessionId(session),
    memberIds: getAssignedMemberIds(session),
    emails: getAssignedEmails(session),
    anyone: getAnyoneCanJoin(session),
  }));
}

async function updateBreakoutAssignments(updateAssignments) {
  await withBreakoutEditLock(async (configuration, requireOwnedLock) => {
    const assignments = createAssignmentState(configuration);

    if (!assignments.length || assignments.some(({id}) => !id)) {
      throw new Error('The current breakout assignments are unavailable.');
    }

    const shouldAssign = await updateAssignments(assignments);
    requireOwnedLock();

    if (shouldAssign !== false) {
      await meeting.breakouts.assign(assignments);
    }
  });
}
```

Use the returned configuration rather than cached `manageGroups`: an incomplete response can leave that cache unchanged. Each session must include a confirmed boolean `anyoneCanJoin`, including an explicit `false`. The SDK's `Breakout` model does not expose this setting. If the response or setting is missing, these helpers stop before changing assignments; refresh and retry instead of substituting a stale value or defaulting to `false`.

Keep one instance of these helpers per meeting, and route automatic assignment, move, exchange, and removal actions through `updateBreakoutAssignments()`. Its shared `withBreakoutEditLock()` runner also coordinates session settings edits. The local guard rejects overlapping actions in one client. The service edit lock coordinates complete-state assignment edits with other host or cohost clients. The SDK maintains the acquired lock and includes its token in `assign()`; the helper rechecks ownership before writing. If acquisition fails or the lock is lost, stop and retry from a newly locked snapshot rather than sending an unlocked payload. Returning `false` from the callback skips `assign()` when the callback performs an unassigned-participant removal instead; the lock does not make unrelated roster mutations transactional.

The helper does not take over a lock retained by another local editing flow. Its `finally` block requests release only for the token acquired by this action. In the current SDK, `unLockEditBreakout()` does not return a promise, so awaiting it cannot confirm release. Keep controls disabled while an action is pending or a local lock token remains. If release is not confirmed, show the retained state and a recovery action; do not clear the SDK's lock state manually or begin another edit with that token.

The final refresh updates `manageGroups` with the confirmed service state. Continue to refresh the rendered roster when `meeting:breakouts:update` fires.

### Assign in-meeting participants

The [move helper below](#move-participants-into-a-session) uses `updateBreakoutAssignments()` to pass the complete array of session assignments to `assign()`, preserving other sessions and their confirmed settings. Each session entry contains the following fields, both before and after sessions start.

| Property | Type | Description |
| --- | --- | --- |
| `id` | String | Target session identifier from the service configuration. |
| `memberIds` | Array | Meeting participant IDs assigned to the session. |
| `emails` | Array | Invitee email addresses assigned to the session. |
| `anyone` | Boolean | Whether unassigned participants can join the session. |

### Track unassigned participants

The SDK does not maintain a separate unassigned collection. Build it in application state by comparing eligible meeting and lobby participants with the IDs assigned to or present in the session rosters. Recalculate this state after every breakout or meeting roster update, including after a remove operation.

Keep meeting and lobby participants in separate presentation groups if your UI distinguishes them. Include a participant only once. Use a meeting participant's SDK ID for assignment actions, and retain email-based preassignments when building the complete payload. Compare both IDs and verified email identities before classifying a participant as unassigned. If their email identity is unresolved, show that state and disable assignment changes for that participant.

### Supply verified participant identities

The SDK's roster `Member` does not expose `email`, `emailAddress`, or a top-level `person.email`. The helpers below instead require application-owned participant inputs containing `id` and `assignmentEmails`. Populate `assignmentEmails` from verified application invite or preassignment records linked to the current roster member. For a resolvable Webex person, the SDK also documents looking up `webex.people.get(member.participant.identity)` and reading the returned person's `emails`; this requires the People plugin and authorized access. Use the person's identity for that lookup, not the meeting member ID.

Verify that the email list includes the aliases used by the participant's preassignments. Guests, missing identity data, unavailable permissions, or incomplete profile aliases may require your application's own verified records. A failed or incomplete lookup is an unknown mapping, not an empty email list. Rebuild these inputs when the meeting or the participant's roster identity changes.

Use `assignmentEmails: []` only when your application has confirmed that the participant has no email-based identity to match. Omit the field while the mapping is unresolved; the helpers reject that input before either assignment or removal. Do not infer identity from a display name.

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

### Move participants to the lobby

Move participants to the main meeting lobby.

```javascript
await meeting.breakouts.moveToLobby([
  {
    participants: ['participant-1'],
  },
]);
```

Both `moveToLobby()` and `removeFromBreakout()` require `mainGroupId` and `mainSessionId`, which the SDK stores from the breakout service response.

### Keep rosters synchronized

The SDK processes live breakout roster events. Request initial rosters after sessions start by calling `queryRosters()`.

```javascript
meeting.breakouts.queryRosters();
```

`queryRosters()` does not return a roster promise. Wait for `meeting:breakouts:update`, then read the current session roster from `meeting.members.membersCollection` and other session rosters from their `Breakout` models.

```javascript
function getSessionMembers(session) {
  const currentSession = meeting.breakouts.currentBreakoutSession;
  const membersCollection = currentSession?.sessionId === session.sessionId
    ? meeting.members.membersCollection
    : session.members?.membersCollection;

  return Object.values(membersCollection?.getAll?.() || {});
}

function refreshBreakoutRosters() {
  const sessions = [...meeting.breakouts.breakouts.models];
  const currentSession = meeting.breakouts.currentBreakoutSession;

  if (
    currentSession?.sessionId &&
    !sessions.some((session) => session.sessionId === currentSession.sessionId)
  ) {
    sessions.push(currentSession);
  }

  sessions.forEach((session) => {
    renderSessionParticipants(session, getSessionMembers(session));
  });

  refreshUnassignedParticipants();
}

meeting.on('meeting:breakouts:update', refreshBreakoutRosters);
meeting.members.on('members:update', refreshBreakoutRosters);
```

Scheduled meetings can contain preassignments. The SDK stores them in `meeting.breakouts.preAssignments` and emits `meeting:breakouts:preAssignmentsUpdate` when they are loaded or changed.

```javascript
function handlePreAssignmentsUpdate() {
  renderPreAssignments(meeting.breakouts.preAssignments);
}

meeting.on(
  'meeting:breakouts:preAssignmentsUpdate',
  handlePreAssignmentsUpdate
);

meeting.breakouts.queryPreAssignments();
```

## Attendee session controls

### Join a session

An attendee can join an active session when its `allowed`, `assigned`, or `requested` state permits joining.

```javascript
const targetSession = meeting.breakouts.breakouts.models.find(
  (session) => session.sessionId === targetSessionId
);

if (!targetSession) {
  throw new Error('The requested breakout session is not available.');
}

await targetSession.join();
```

The `requested` property indicates that a host asked the attendee to move to that session. Refresh the UI from each update event instead of retaining a stale requested-session reference.

### Leave a session

Return from the current breakout session to the main meeting.

```javascript
if (!meeting.breakouts.isInMainSession) {
  await meeting.breakouts.currentBreakoutSession.leave();
}
```

Calling `leave()` while already in the main session throws an error. Applications should also respect `allowBackToMain` when deciding whether to display a Leave control.

### Ask for help

An attendee in a breakout session can request help from the host or cohost.

```javascript
if (meeting.breakouts.isActiveBreakout) {
  await meeting.breakouts.currentBreakoutSession.askForHelp();
}
```

Hosts and cohosts receive `meeting:breakouts:askForHelp` with the participant and session identifier. Disable repeated requests while one is pending to avoid duplicate notifications.

## Broadcast messages and request return

### Broadcast to all sessions

Send a message to every active breakout session.

```javascript
await meeting.breakouts.broadcast(
  'The sessions will end in five minutes.'
);
```

Omit options to send the message without a role filter. The supported role filters are `cohosts` and `presenters`.

```javascript
await meeting.breakouts.broadcast('Host update', {
  cohosts: true,
  presenters: true,
});
```

### Broadcast to one session

Call `broadcast()` on a `Breakout` model to target one session.

```javascript
await targetSession.broadcast('Please select a presenter.');
```

Receive messages through the meeting event. Treat message text as untrusted user content and render it as text, not HTML.

```javascript
function handleBreakoutMessage(event) {
  showBreakoutMessage({
    message: event.message,
    senderUserId: event.senderUserId,
    sentTime: event.sentTime,
  });
}

meeting.on('meeting:breakouts:message', handleBreakoutMessage);
```

In the current SDK implementation, `event.sessionId` is populated from the receiver's `currentBreakoutSession`. It is not guaranteed to identify the session that originally received the broadcast, so do not use it to route or authorize a message.

### Ask everyone to return

Request that all breakout participants return to the main meeting.

```javascript
await meeting.breakouts.askAllToReturn();
```

Attendees receive `meeting:breakouts:askReturnToMain`. Their application should display the request and use `currentBreakoutSession.leave()` when the attendee returns.

```javascript
function handleAskReturnToMain() {
  showReturnToMainRequest();
}

meeting.on('meeting:breakouts:askReturnToMain', handleAskReturnToMain);
```

## Reset breakout sessions

Reset is an application workflow rather than a single SDK call. If sessions are active, end them and wait until the SDK reports that they are closed. Then call `clearSessions()` and reset local form, selection, and roster state.

```javascript
function waitForBreakoutsToClose(timeoutMs = 10000) {
  if (!meeting.breakouts.isBreakoutInProgress()) {
    return Promise.resolve();
  }

  return new Promise((resolve, reject) => {
    const handleUpdate = () => {
      if (!meeting.breakouts.isBreakoutInProgress()) {
        window.clearTimeout(timeoutId);
        meeting.off('meeting:breakouts:update', handleUpdate);
        resolve();
      }
    };

    const timeoutId = window.setTimeout(() => {
      meeting.off('meeting:breakouts:update', handleUpdate);
      reject(new Error('Timed out waiting for breakout sessions to close.'));
    }, timeoutMs);

    meeting.on('meeting:breakouts:update', handleUpdate);
    handleUpdate();
  });
}

if (meeting.breakouts.isBreakoutInProgress()) {
  await meeting.breakouts.end({delayCloseTime: 0});
  await waitForBreakoutsToClose();
}

await meeting.breakouts.clearSessions();
resetBreakoutUIState();
```

Do not clear the application UI before `clearSessions()` succeeds. If the service request fails, preserve the last confirmed state and provide a retry action.

## Breakout events

Register these events on the `Meeting` object with `meeting.on()`.

| Event | Payload | Description |
| --- | --- | --- |
| `meeting:breakouts:update` | None | Breakout configuration, local assignment state, or roster information changed. Read the latest state from `meeting.breakouts`. |
| `meeting:breakouts:closing` | None | Active breakout sessions entered the closing state. |
| `meeting:breakouts:message` | `{senderUserId, sentTime, message, sessionId}` | A breakout broadcast message was received. `sessionId` reflects the receiver's current session and is not guaranteed to identify the broadcast target. |
| `meeting:breakouts:askReturnToMain` | None | The host or cohost requested that attendees return to the main meeting. |
| `meeting:breakouts:leave` | None | The local user moved from a breakout session to the main meeting. |
| `meeting:breakouts:askForHelp` | `{participant, sessionId}` | A participant requested help from the host or cohost. |
| `meeting:breakouts:preAssignmentsUpdate` | None | Scheduled breakout preassignment data was loaded or changed. Read it from `meeting.breakouts.preAssignments`. |

Remove listeners when the meeting view is destroyed to prevent duplicate handlers.

```javascript
meeting.off('meeting:breakouts:update', refreshBreakoutUI);
meeting.off('meeting:breakouts:update', handleBreakoutInvitation);
meeting.off('meeting:breakouts:update', refreshBreakoutRosters);
meeting.members.off('members:update', refreshBreakoutRosters);
meeting.off(
  'meeting:breakouts:preAssignmentsUpdate',
  handlePreAssignmentsUpdate
);
meeting.off('meeting:breakouts:message', handleBreakoutMessage);
meeting.off('meeting:breakouts:askReturnToMain', handleAskReturnToMain);
```

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

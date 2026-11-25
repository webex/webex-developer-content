---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Update session settings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions). [Full Markdown](../../../../docs/sdks-webex-meetings-sdk-web-breakout-sessions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use the Webex Web Meetings SDK to configure, manage, and monitor breakout sessions for hosts, cohosts, and attendees.

## Selected section

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

`updateBreakoutSession()` checks the selected session against the returned configuration and includes the group ID in `update()`. Passing `false` as the second argument retains the token until the shared runner refreshes state and requests release in `finally`. Keep controls disabled while an edit is pending or a local token remains; the release behavior is described in [Build the current assignment payload](https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions#build-the-current-assignment-payload).

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

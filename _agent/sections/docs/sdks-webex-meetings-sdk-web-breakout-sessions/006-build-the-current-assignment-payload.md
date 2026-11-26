---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-meetings-sdk-web-breakout-sessions
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage participants
- Build the current assignment payload
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

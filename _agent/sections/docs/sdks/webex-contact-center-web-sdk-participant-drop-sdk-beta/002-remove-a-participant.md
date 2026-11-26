---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Remove a participant
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Participant Drop lets the primary agent remove an eligible participant from an active Webex Contact Center voice conference. Use the voice task's `dropConferenceParticipant` method, then refresh your application from the updated task rather than removing a participant from the UI immediately.

## Selected section

## Remove a participant

Call the method on the current voice task with a non-empty participant identifier:

```javascript
task.on('task:participantLeft', (updatedTask) => {
  // Refresh the participant list from updatedTask.data.interaction.
});

try {
  await task.dropConferenceParticipant({participantId});
} catch {
  // Keep the participant visible and show a generic error.
}
```

The promise resolves when the service confirms that the participant left. It rejects if the request fails or times out. The existing `task:participantLeft` event provides the updated task for roster changes; do not remove a row optimistically. If your application replaces a task after a merge, attach its task listeners to the current task. See [Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks) and [Events](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-events) for the broader task lifecycle.

Only the backend-selected primary agent should be offered Drop for eligible targets. In the [Contact Center SDK sample source](https://github.com/webex/webex-js-sdk/tree/next/docs/samples/contact-center), Agent and joined Entry Point/dial-number (EP-DN) targets use their participant identifier. For Customer, the sample uses the inbound ANI or outbound DNIS. Supervisor rows are visible but cannot be dropped. The sample asks for confirmation before Customer Drop, locks other Drop actions while a request is pending, and disables them during an active, non-held consult. These are sample-application safeguards; backend authorization remains authoritative.

When ownership changes, use the updated task's `interaction.owner` to refresh primary-agent permissions. Do not elect a new owner in the client.

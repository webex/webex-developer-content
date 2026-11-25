---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Integrate mid-call summaries
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Integrate mid-call summaries

### Generate and share a summary

Use the initiating agent's active task when preparing a consult or transfer:

1. Check `task.aiSummaryCapabilities.midCallEnabled` and the normal task-state and destination requirements for the call operation.
2. Call `task.requestMidCallSummary(action)` with an `AISummaryAction` of `'CONSULT'` or `'TRANSFER'`. The promise resolves to an `AISummary` for your application to display.
3. Let the agent review and edit the content. Build an `AISummaryResponse` with the reviewed summary, feedback, response state, and actual view, edit, and copy counts. See [Summary payloads and responses](https://developer.webex.com/docs/sdks/ai-summaries#summary-payloads-and-responses).
4. Dispatch `task.sendMidCallSummaryResponse(response, action)` with the same action used for generation, and handle its result.
5. Start the consult or transfer through the existing task API.

Summary reporting and call control are separate operations. A reporting acknowledgement confirms the report was accepted; it does not start the consult or transfer or confirm delivery to the receiving agent. The call operation can proceed independently of that acknowledgement, provided your application handles reporting failures.

If the agent cancels the consult or transfer selection, report the appropriate response state. Sending `'MID_CALL_CANCELLED'` does not cancel generation or an active call operation. After a successful consult or transfer submission, closing its dialog should not send a second cancellation response.

### Display a received summary

The receiving task emits `TASK_EVENTS.TASK_MID_CALL_SUMMARY_RECEIVED` with an `AISummary`. The receiving agent does not need to request generation to view it.

Display the event payload for that task, provide a notification and a way to reopen it, and keep received content distinct from summaries the agent subsequently generates. Your application controls summary display and any retained history. Previously delivered summaries are not guaranteed to replay.

### Report receiving-agent feedback

Receiving-agent card actions use `webex.cc.apiAIAssistant.sendEvent()`. Use this event path for feedback on a received card; `task.sendMidCallSummaryResponse()` reports the initiating agent's consult or transfer response.

| Argument | Value |
| --- | --- |
| Agent ID | Authenticated receiving agent's ID. |
| Interaction ID | `task.data.interactionId` from the receiving task. |
| Event type | `CUSTOM_EVENT`. |
| Event name | `MID_CALL_SUMMARY_USER_ACTION`. |
| Event metadata | `{adaptiveCardId: summary.adaptiveCardId, userAction: {actionType: 'Action.Submit', actionId}}`. |
| Language code | `summary.languageCode`, or `en` when absent. |
| Tracking ID | `summary.trackingId` when it is a string; otherwise omit it. |

Use `likeButton`, `dislikeButton`, and `copyButton` as the action IDs for positive feedback, negative feedback, and copying.

Require a card ID and associate each submission with the displayed summary and its receiving interaction, including retained history. Prevent overlapping submissions for the same card. Confirm feedback only after a successful send and preserve the previous selection on failure; a later summary must not receive an earlier card's acknowledgement.

**Beta typing limitation:** SDK `3.12.0-next.159` exposes `sendEvent()`, but its event-name type union omits `MID_CALL_SUMMARY_USER_ACTION`. A direct TypeScript integration needs a narrow type assertion on that argument.

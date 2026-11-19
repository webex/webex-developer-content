---
type: Guide
title: Webex Contact Center SDK AI-generated Summaries Beta
display_title: AI Summaries Beta
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ai-summaries)

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Beta overview

AI Summaries Beta is available in `@webex/contact-center@3.12.0-next.159` and supports two workflows:

| Workflow | Agent experience |
| --- | --- |
| Mid-call summary | Generate and review a summary before an agent-to-agent consult or transfer. The receiving agent can view the shared summary. |
| Post-call summary | Review and edit a summary during wrap-up, with suggested wrap-up reasons when available. |

The SDK provides summary generation, response reporting, capability updates, and an event for received mid-call summaries. Your application provides the review UI, editing, notifications, feedback, and usage tracking. Consult, transfer, and task wrap-up use their existing task APIs.

## Before you begin

- **Configure AI Assistant.** An administrator must enable AI Assistant access and the required summary features for the applicable queues. See [Enable AI Assistant features in Control Hub for Webex Contact Center](https://help.webex.com/article/n9lk3t6/Enable-Cisco-AI-Assistant-for-Contact-Center) for licensing, user-profile, and recording prerequisites. Its Agent Desktop layout and notification instructions apply to Agent Desktop; SDK applications provide their own UI.
- **Check language availability.** See the **Supported languages for Summaries** table in [Multi-language Support for AI Assistant Features](https://help.webex.com/article/nlm6pob/Multi-language-Support-for-AI-Assistant-Features). Availability depends on the feature, locale, and SKU.
- **Initialize an agent session.** Complete authentication, SDK initialization and readiness, registration, and station login. See [Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication). Use the pinned Beta package below in place of the Quickstart's unversioned installation command.
- **Obtain the agent's task.** Follow the [task lifecycle](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks) to obtain an `ITask` for new and restored interactions. The examples in this guide begin with an initialized session and an existing task.

Install the Beta package with npm or Yarn:

```bash
npm install @webex/contact-center@3.12.0-next.159
# Alternative
yarn add @webex/contact-center@3.12.0-next.159
```

## Check summary availability

Generation requires both the organization-level configuration flag and the corresponding task capability:

| Feature | Contact Center configuration | Task capability |
| --- | --- | --- |
| Mid-call | `generatedSummaries.consultTransferSummariesEnabled === true` | `task.aiSummaryCapabilities.midCallEnabled === true` |
| Post-call | `generatedSummaries.wrapUpSummariesEnabled === true` | `task.aiSummaryCapabilities.postCallEnabled === true` |

The SDK rejects a request if either gate is missing or false. Configure organization flags through Contact Center; use the task capability snapshot and updates to control generation actions in your UI. The summary APIs add no station or destination restrictions beyond those of the underlying call flow and tenant configuration.

Both task capabilities initially default to `false`. Read `task.aiSummaryCapabilities` when binding a task and subscribe to `TASK_EVENTS.TASK_FEATURE_ENABLEMENT` for subsequent changes. Reading the snapshot also handles an update that arrived before listener registration.

Bind the received-summary listener at the same time, independently of generation controls. Attach it before answering an offered call: a late listener or restored session is not guaranteed to receive previously delivered summaries.

```typescript
import {TASK_EVENTS} from '@webex/contact-center';
import type {
  AISummary,
  AISummaryFeatureEnablement,
  ITask,
} from '@webex/contact-center';

export function bindSummaries(
  task: ITask,
  updateAvailability: (midCall: boolean, postCall: boolean) => void,
  showReceivedSummary: (summary: AISummary) => void
): () => void {
  const refresh = (_event?: AISummaryFeatureEnablement): void => {
    const {midCallEnabled, postCallEnabled} = task.aiSummaryCapabilities;
    updateAvailability(midCallEnabled, postCallEnabled);
  };

  task.on(TASK_EVENTS.TASK_FEATURE_ENABLEMENT, refresh);
  task.on(TASK_EVENTS.TASK_MID_CALL_SUMMARY_RECEIVED, showReceivedSummary);
  refresh();

  return () => {
    task.off(TASK_EVENTS.TASK_FEATURE_ENABLEMENT, refresh);
    task.off(TASK_EVENTS.TASK_MID_CALL_SUMMARY_RECEIVED, showReceivedSummary);
  };
}
```

Call the cleanup function when replacing the task or unmounting its view. Associate displayed summaries and pending results with their originating task so an old result cannot update another interaction.

## Integrate mid-call summaries

### Generate and share a summary

Use the initiating agent's active task when preparing a consult or transfer:

1. Check `task.aiSummaryCapabilities.midCallEnabled` and the normal task-state and destination requirements for the call operation.
2. Call `task.requestMidCallSummary(action)` with an `AISummaryAction` of `'CONSULT'` or `'TRANSFER'`. The promise resolves to an `AISummary` for your application to display.
3. Let the agent review and edit the content. Build an `AISummaryResponse` with the reviewed summary, feedback, response state, and actual view, edit, and copy counts. See [Summary payloads and responses](#summary-payloads-and-responses).
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

## Integrate post-call summaries

Request a post-call summary on the task being wrapped up:

1. Check `task.aiSummaryCapabilities.postCallEnabled`, then await `task.requestPostCallSummary()`.
2. Display the returned `AISummary`. Let the agent review and edit it, record feedback and usage, and select a configured wrap-up reason.
3. Build an `AISummaryResponse`. If reporting the selected reason, set the optional `response.wrapUpCode` to its configured code identifier (`auxCodeId`).
4. Dispatch `task.sendPostCallSummaryResponse(response)` before task cleanup and handle its result.
5. Complete wrap-up separately with `task.wrapup({wrapUpReason, auxCodeId})`, using the selected reason's label and configured identifier.

Wrap-up can start without waiting for summary-reporting acknowledgement. Handle both results independently, including when your application performs automatic wrap-up. Post-call summaries are returned by the request promise; there is no post-call-summary-received task event.

### Use suggested wrap-up reasons

`summary.suggestedWrapUpCodes` optionally contains suggested reasons, and `summary.suggestedWrapUpCodesMessage` optionally provides explanatory text. Each suggestion declares a `name`; it may not contain a configured code identifier. Match the suggestion to a valid configured reason before using it.

Suggestions do not select a reason or complete wrap-up automatically. Keep manual reason selection available when suggestions are absent or have no configured match. Summary content and wrap-up suggestions can be available independently.

## Summary payloads and responses

### Task API reference

| Method | Result |
| --- | --- |
| `requestMidCallSummary(action)` | `Promise<AISummary>` for `'CONSULT'` or `'TRANSFER'`. |
| `sendMidCallSummaryResponse(response, action)` | `Promise<void>` acknowledging the consult or transfer summary report. |
| `requestPostCallSummary()` | `Promise<AISummary>` for post-call review. |
| `sendPostCallSummaryResponse(response)` | `Promise<void>` acknowledging the post-call summary report. |

### Render available content

`AISummary` requires `conversationId`; its content fields are optional. Render the fields present in the payload rather than assuming a fixed sentence or format.

| Field | Handling |
| --- | --- |
| `sections` | Structured text: `reasonForTransferOrConsult`, `initialContactReason`, `additionalContactReasons`, `additionalContext`, `keyActionsTaken`, and `nextSteps`. Preserve the keys when reporting edited sections. |
| `summaryText` | Plain-text fallback when structured text is unavailable. |
| `adaptiveCard` and `editAdaptiveCard` | Optional card content. Render supported formats in your application; a card-only payload can contain usable content. |
| `suggestedWrapUpCodes` and `suggestedWrapUpCodesMessage` | Optional wrap-up suggestions and explanatory text. |

Check other optional fields before use. For example, the type does not require a sender name or a consult/transfer action field.

### Build the response

Every `AISummaryResponse` requires:

| Field | Value |
| --- | --- |
| `summary` | Reviewed structured sections or a string. |
| `feedback` | `'none'`, `'thumbs_up'`, or `'thumbs_down'`. |
| `state` | A response state from the table below. |
| `numberOfTimesViewed` | Actual view count. |
| `numberOfTimesEdited` | Actual edit count. |
| `numberOfTimesCopied` | Actual copy count. |

The SDK reports the supplied values; your application manages response state and usage counts. The table below is an example UI policy for the supported state values, rather than behavior applied automatically by the SDK:

| State | Application policy |
| --- | --- |
| `DEFAULT` | Content is available and included. |
| `EXCLUDED` | The initiating agent opts out of including the summary in the next consult or transfer submission. |
| `IGNORED` | No content is available, including while generation is pending, unless exclusion or failure determines the state. |
| `NOT_RECEIVED` | Generation failed without producing content; takes precedence over exclusion. |
| `MID_CALL_CANCELLED` | The agent cancels the consult or transfer selection. |

An exclusion choice is local until reporting. Keep the content available and preserve the choice across generation or retry. `EXCLUDED` records the choice for that submission; it does not establish a recipient access policy.

`wrapUpCode` is optional for post-call reporting. The optional `summaryReceived` field is not transmitted by these response methods in this SDK version and cannot serve as a delivery acknowledgement. Your application does not need to supply transport timestamps.

This helper creates an initial response from structured or plain text. Replace the draft with agent-reviewed content and update feedback, state, and counts before reporting:

```typescript
import type {AISummary, AISummaryResponse} from '@webex/contact-center';

export function createSummaryResponse(
  summary: AISummary
): AISummaryResponse | undefined {
  const hasSectionText = Object.values(summary.sections ?? {}).some(
    (value) => typeof value === 'string' && value.trim().length > 0
  );
  const content = hasSectionText ? {...summary.sections} : summary.summaryText;
  if (!content || (typeof content === 'string' && content.trim().length === 0)) {
    return undefined;
  }

  return {
    summary: content,
    feedback: 'none',
    state: 'DEFAULT',
    numberOfTimesViewed: 0,
    numberOfTimesEdited: 0,
    numberOfTimesCopied: 0,
  };
}
```

The helper returns `undefined` when it finds no usable structured or plain text, including for card-only payloads. Handle supported card content separately or show an unavailable-content state; do not submit an empty default response.

## Beta limitations and error handling

- **Concurrent operations:** Allow one pending mid-call generation request per conversation, shared across consult and transfer actions, and one pending post-call request. Prevent duplicate reports while a submission is pending. Restore controls after success or failure.
- **Cancellation and lifecycle:** There is no dedicated public summary-request cancellation method. Remove listeners when their view is released, and ignore late results after the task changes or the session ends. Manage displayed content and retained history explicitly, and clear conversation content on logout.
- **Retries:** Handle generation and reporting rejections explicitly. A failed refresh can leave previously displayed content available. Offer a user-triggered generation retry without overlapping requests; do not assume automatic reporting retries.
- **Inputs and diagnostics:** Validate caller-supplied actions and response values. Treat rejected values as `unknown`, since not every error contains `data.errorCode`. Keep tokens and conversation content out of diagnostics.

| Symptom or error | Recovery |
| --- | --- |
| `MID_CALL_SUMMARY_DISABLED` or `POST_CALL_SUMMARY_DISABLED` | Check both the organization flag and task capability. |
| `MID_CALL_SUMMARY_TIMEOUT` or `POST_CALL_SUMMARY_TIMEOUT` | Show the failure state, restore controls, and offer a manual generation retry where appropriate. |
| `AI_ASSISTANT_BASE_URL_NOT_AVAILABLE` | Check registration, environment configuration, and AI Assistant availability with the environment owner. |
| Task removal or session end during a request | Handle rejection and discard results that no longer belong to the active interaction. |
| No summary on the receiving agent | Check the destination, summary inclusion, completed consult or transfer, receiving task, and listener binding. Generation success alone does not confirm delivery. |
| Other generation or reporting failure | Handle the rejection independently of call control and record a diagnostic without credentials or summary content. |

## Try the Beta and verify your integration

Use the [Contact Center SDK sample](https://web-sdk.webex.com/samples/contact-center/) with an eligible test tenant, an authorized caller, two eligible agent sessions for consult and transfer, and a configured wrap-up reason. The hosted sample's deployed SDK version can differ from this guide's pinned Beta; check its build before testing.

In **Auth & Registration**, choose the environment and SDK toggles, supply an authorized test agent's access token, select **webex.init()**, then **webex.cc.register()**, and wait for completion. In **Agent Station Login/Logout**, select a permitted team and station option, select **Login**, and set the agent to Available.

Watch [sdk ai summaries — 1 minute 34 seconds](https://app.vidcast.io/share/cf7c0bc6-1dd5-4ae1-aabe-f1438a98d1e3), by Ravi Chandra Sekhar Sarika, for a walkthrough of consult-summary generation, receiving-agent display, and post-call review, editing, feedback, and wrap-up. Your application must invoke the generation methods; binding listeners alone does not generate summaries.

Validate the following in your configured Beta environment. Record the SDK build, setup, and observed result, then complete the test calls and session cleanup.

| Area | Verify |
| --- | --- |
| Availability and lifecycle | Controls reflect both the initial capability snapshot and updates. New and restored tasks have listeners; task changes do not display stale results. |
| Consult and transfer | Both actions generate content, preserve reviewed edits, and report with the matching action. Verify the call operation and receiving-agent content separately. |
| Review and feedback | View, edit, and copy counts reflect agent actions. Exclusion, cancellation, and receiving-card feedback use the intended response or event values. |
| Post-call wrap-up | Reporting and wrap-up complete independently. Suggested reasons map to configured codes, and manual selection works without suggestions. |
| Content and failures | Handle structured text, plain text, supported cards, and missing content. Test disabled features, timeouts, duplicate submissions, and session changes during pending work. |

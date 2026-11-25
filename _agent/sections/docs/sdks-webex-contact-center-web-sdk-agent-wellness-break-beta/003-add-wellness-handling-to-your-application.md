---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add wellness handling to your application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta). [Full Markdown](../../../../docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break with the Webex Contact Center SDK. The SDK delivers wellness events and actions. Your application presents the break, waits for active work to finish, and returns the agent to Available.

## Selected section

## Add wellness handling to your application

### Register and listen for events

Add this fragment to the async setup function that registers Contact Center. Check the effective flag, get the system idle code, and listen for the validated wellness event. The UI functions are placeholders for your application code.

```js
import {CC_AGENT_EVENTS} from '@webex/contact-center';

const profile = await webex.cc.register();
if (!profile.isWellnessBreakEnabled) return;

const wellbeingCode = await webex.cc.getWellbeingBreakIdleCode();
const WELLNESS_REQUEST_DECISION_TIMEOUT_MS = 5 * 60 * 1000;
let pendingManualRequest;

function clearManualRequest() {
  if (pendingManualRequest) clearTimeout(pendingManualRequest.timer);
  pendingManualRequest = undefined;
}

const onWellnessBreak = (event) => {
  if (event.actionEvent === 'SUGGEST_WELLNESS_BREAK') {
    clearManualRequest();
    showRequestAction();
  } else if (event.actionEvent === 'PROVIDE_WELLNESS_BREAK') {
    if (pendingManualRequest) {
      clearManualRequest();
      beginApprovedBreak(event);
    } else {
      showDirectOffer(event);
    }
  } else if (event.actionEvent === 'WELLNESS_BREAK_NOT_ALLOWED') {
    clearManualRequest();
    hideRequestAction();
    showRequestDenied(event.actionText);
  }
};

webex.cc.on(CC_AGENT_EVENTS.WELLNESS_BREAK, onWellnessBreak);

function stopWellnessHandling() {
  clearManualRequest();
  webex.cc.off(CC_AGENT_EVENTS.WELLNESS_BREAK, onWellnessBreak);
}
```

A fresh suggestion clears any earlier pending request and its timer before showing the request action. Handle `WELLNESS_BREAK_NOT_ALLOWED` even when no request is pending. Implement `hideRequestAction()` to remove or disable the request control until a new suggestion arrives.

`PROVIDE_WELLNESS_BREAK` has no separate field that distinguishes approval from a direct offer. Your application must track whether it has a manual request pending. Treat `actionText` as plain text. Do not log the full notification.

Call `stopWellnessHandling()` on logout, deregistration, host unmount, or a change to the active station session. This clears the pending request and its timer and removes the listener. Set up fresh wellness handling for the next session.

### Request a break

Show the request action only after `SUGGEST_WELLNESS_BREAK`. Call this handler from the request button. HTTP 202 means that the service received the action; it does not mean that the break was approved. After HTTP acceptance, wait for a separate approval or denial for up to five minutes, as the SDK sample does.

```js
async function requestBreak() {
  if (pendingManualRequest) return;

  const request = {timer: undefined};
  pendingManualRequest = request;
  try {
    await webex.cc.apiAIAssistant.requestWellnessBreak();
    if (pendingManualRequest !== request) return;

    request.timer = setTimeout(() => {
      if (pendingManualRequest !== request) return;
      clearManualRequest();
      showRequestTimedOut();
    }, WELLNESS_REQUEST_DECISION_TIMEOUT_MS);
  } catch (error) {
    if (pendingManualRequest !== request) return;
    clearManualRequest();
    throw error;
  }
}
```

Implement `showRequestTimedOut()` to clear the pending display and explain that no decision arrived. The five-minute timeout controls how long the application waits. It does not cancel the backend request, send a wellness action, or change the agent state. Do not retry automatically. After timeout, handle the next `PROVIDE_WELLNESS_BREAK` as a direct offer.

The example compares request objects so a late HTTP result cannot restart a timer or clear a newer request after cleanup.

After a pending request is approved, enter the wellness state and run the break. Do not call `respondToWellnessBreak({action: 'ACCEPTED'})` for this path.

### Respond to a direct offer

For a direct offer, request the **Idle** state with the system `WellbeingBreak` code. Send `ACCEPTED` only after that request succeeds. Confirm the observed state and wait for active work and wrap-up to finish before starting the break timer.

```js
await webex.cc.setAgentState({
  state: 'Idle',
  auxCodeId: wellbeingCode.id,
});
await webex.cc.apiAIAssistant.respondToWellnessBreak({
  action: 'ACCEPTED',
});
```

If the agent selects **Later**, send `REJECTED`. If the offer times out, send `NO_RESPONSE`. Send only one response for an offer. Neither action changes the agent state. `REQUESTED` is sent only by `requestWellnessBreak()`.

The SDK supplies the active agent and station session for both wellness methods. The `agentSessionId` on an incoming notification is diagnostic data and can differ from the active session. Do not copy identity fields from the notification into an action.

### End the break

Your application owns the timer, task checks, and recovery. When the break ends, return the agent to **Available**, regardless of the state held before the break.

```js
await webex.cc.setAgentState({
  state: 'Available',
  auxCodeId: '0',
});
```

Keep restoration tied to the station session that entered the break. Confirm Available before clearing recovery state. If entering `WellbeingBreak` fails, do not send `ACCEPTED`. If an action fails after entering that state, request Available and surface the error. Stop old timers and listeners after logout or a session change.

### Complete lifecycle example

The [Contact Center sample implementation](https://github.com/webex/webex-js-sdk/blob/v3.12.0-next.220/docs/samples/contact-center/app.js) shows how to route wellness events, wait for active tasks and wrap-up, run the break timer, restore Available, and stop work after logout or a session change. Its [wellness lifecycle helpers](https://github.com/webex/webex-js-sdk/blob/v3.12.0-next.220/docs/samples/contact-center/wellness-utils.js) define the transition and recovery rules. Use these files with the SDK calls above when you implement the full flow.

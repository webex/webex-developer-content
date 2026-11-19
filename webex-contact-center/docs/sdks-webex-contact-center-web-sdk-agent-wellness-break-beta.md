---
type: Guide
title: Webex Contact Center Web SDK | Agent Wellness Break Beta
display_title: Agent Wellness Break Beta
canonical_url: https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta)

Use this guide to test Agent Wellness Break with the Webex Contact Center SDK. The SDK delivers wellness events and actions. Your application presents the break, waits for active work to finish, and returns the agent to Available.

## Before you begin

- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use an approved Contact Center organization and agent.
- Confirm that the organization has an AI Assistant entitlement and that agent wellbeing and wellness break reminders are enabled. The SDK reports the effective result as `profile.isWellnessBreakEnabled`. Your application does not need a separate wellness feature toggle.
- Use `@webex/contact-center` **3.12.0-next.133**. If your application uses the `webex` aggregate package, use **3.12.0-next.220**. Pin these package versions for this beta.
- Complete the [Webex Contact Center Web SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). Register the SDK and complete station login or relogin before sending a wellness action.
- Use one active agent session per SDK instance. This beta does not support multiple sessions or organizations in one instance.

Wellness events arrive through the AI Assistant real-time connection. The SDK opens that connection when the effective wellness flag is true, even if transcripts and suggested responses are disabled. A missed offer is not replayed after a connection interruption.

Watch the [SDK wellness demonstration](https://app.vidcast.io/share/aec5197c-5bbe-4d1a-b2f3-a193adb64853) for an example of the test flow.

## Test with the SDK sample application

Use the beta sample build supplied with your invitation. Confirm that it includes the SDK version listed above before you test. The sample uses live wellness events; it does not create mock offers.

1. Sign in as the beta test agent and initialize the sample with a temporary developer access token. Do not put the token in a screenshot or test report.
2. Register the SDK, complete station login, and set the agent to **Available**. Confirm that `isWellnessBreakEnabled` is true and that the system idle code is named `WellbeingBreak`.
3. Wait for `SUGGEST_WELLNESS_BREAK`. Select **Take wellbeing break** once. Confirm that the request stays pending after HTTP acceptance. Wait for a separate `PROVIDE_WELLNESS_BREAK` approval or `WELLNESS_BREAK_NOT_ALLOWED` denial. If no decision arrives within five minutes, confirm that the sample clears the pending request and shows a timeout message.
4. After approval, confirm that the sample enters **Idle** with the `WellbeingBreak` code. It must not send a second `ACCEPTED` action for an approved manual request.
5. Test a direct `PROVIDE_WELLNESS_BREAK` offer with no request pending. Accept it and confirm that the state-change request succeeds before the sample sends `ACCEPTED`. Test **Later** and the response timeout separately; each must send only one response and leave the agent state unchanged.
6. Accept a break during an active voice or digital task. Confirm that the break timer waits for the task and required wrap-up to finish.
7. Let the break end. Confirm that the agent returns to **Available** with aux code `0`. `WellbeingBreak` must not appear as a normal selectable idle code.
8. Repeat after logout, relogin, and a connection interruption. Confirm that a new live event works and that a missed offer does not reappear.

The test passes when the request and direct-offer paths use the correct actions, the break waits for work to finish, and the agent returns to Available.

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

## Validate the integration

- A suggestion enables one manual request. HTTP acceptance leaves the UI pending until a later approval or denial event, or until the five-minute decision timeout.
- A fresh suggestion clears an earlier pending request and its timer and enables a new request.
- A denial clears pending state and disables the request action, even if no request is pending.
- A missing decision clears pending UI after five minutes. A later direct offer follows the direct-offer path and sends the appropriate response.
- A pending request approved by `PROVIDE_WELLNESS_BREAK` starts the state-change flow without a second `ACCEPTED` action.
- A direct offer sends one of `ACCEPTED`, `REJECTED`, or `NO_RESPONSE`. Acceptance follows a successful state-change request.
- Active work and wrap-up finish before the break timer starts. Completion returns the agent to Available with aux code `0`.
- Logout or a station-session change clears pending UI and its timer, and prevents late results or recovery from acting on a later session.

## Troubleshoot the test

- **The feature is unavailable:** Check the AI Assistant entitlement, wellbeing and reminder settings, the SDK version, station login, and `profile.isWellnessBreakEnabled`. Register again after the organization configuration changes.
- **A request stays pending:** HTTP 202 confirms receipt only. Wait for `PROVIDE_WELLNESS_BREAK` or `WELLNESS_BREAK_NOT_ALLOWED`. If no decision arrives within five minutes, clear the pending UI without changing the agent state or sending `NO_RESPONSE`. Check that the real-time connection and active session are current; do not retry automatically.
- **A wellness action fails:** Complete station login or relogin. The action methods do not accept an agent or session override.
- **The break does not start or end:** Check the observed `WellbeingBreak` state, active tasks, wrap-up, timer, and Available restoration. Do not start a timer based on HTTP acceptance alone.

## Share feedback

Use the feedback channel supplied with your beta invitation. Include the test time and time zone, SDK version, event type, lifecycle phase, expected result, actual result, and a non-sensitive error code or tracking ID. Do not include access tokens, agent names, notification text, or customer content.

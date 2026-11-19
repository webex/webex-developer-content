---
type: Guide
title: Webex Contact Center Web SDK | Participant Drop with the Webex Contact Center SDK (Beta)
display_title: Participant Drop with the Webex Contact Center SDK (Beta)
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta)

Participant Drop lets the primary agent remove an eligible participant from an active Webex Contact Center voice conference. Use the voice task's `dropConferenceParticipant` method, then refresh your application from the updated task rather than removing a participant from the UI immediately.

## Before you begin

- Complete the [Web SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication). Register each test agent, complete station login, and confirm that they can receive voice tasks.
- Use an approved beta SDK build and a Webex Contact Center organization where the routing service supports Participant Drop. There is no client-side SDK feature flag; the service decides whether a request is authorized.
- Prepare a test customer and at least three test agents so you can check conference, ownership-change, and consult scenarios without using real customer data.

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

## Test the beta feature

Watch the [SDK sample walkthrough](https://app.vidcast.io/share/ad03db28-985b-492b-8ba3-ae4d20a6e3f3), then use the SDK sample or your existing integration to test the following:

In the SDK sample, enter your access token, select `webex.init()`, and then select `webex.cc.register()` before starting the call scenarios.

![Contact Center SDK sample showing the Access Token field, webex.init button, and webex.cc.register button in sequence.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbbc4715a32c3ce62/6ac383ce517fb6d0c9971dfb/participant-drop-sdk-sample-setup.png)

*SDK sample setup. The screenshot shows an empty token field before initialization and registration.*

1. **Create a conference.** Start a customer voice call, consult another agent, and merge. Confirm the primary and secondary agents see the expected participants.
2. **Check permissions.** The primary agent can request Drop for eligible Customer, Agent, and joined EP-DN targets. A secondary agent cannot initiate Drop; a Supervisor remains view-only.
3. **Drop another agent.** Confirm the selected agent leaves, the remaining call continues, and the roster changes only after the task update. If only the primary agent and Customer remain, the sample returns to its normal one-to-one view.
4. **Test Customer confirmation.** Cancel once, including with Escape, and confirm the Customer stays connected. Then confirm Drop; only the Customer should leave. The sample keeps its Participants section when another supported participant remains.
5. **Test consult and owner changes.** During an active non-held consult, check that sample Drop controls are disabled; hold or end the consult and check them again. Have the primary agent leave and verify the backend-selected new owner appears on the surviving agents' updated tasks.
6. **Test a nested consult.** While a secondary agent consults a third agent before merge, drop that secondary agent from the primary agent's view. Check the affected call views in both ringing and answered cases, and report any call that remains visible after removal.
7. **Test failure and cleanup.** On a failed or timed-out request, the participant must remain listed until an authoritative update arrives, and the application should restore its controls and show a generic error. End or wrap up the task and check that the participant UI clears.

## Troubleshooting and feedback

If Drop is unavailable, check that the task is an active voice conference, the current agent is the backend-selected primary owner, the target has joined the main conference, and the organization is enabled. For a rejected request, wait for it to settle before retrying; do not infer success from the button click.

Report the scenario, expected and actual result, approximate time and time zone, browser, operating system, SDK build, and whether the agent was primary or secondary. Include a non-sensitive tracking reference if available. Do not send access tokens, credentials, names, full phone numbers, participant identifiers, authorization headers, request URLs, or raw routing payloads.

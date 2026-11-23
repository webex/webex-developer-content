---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Test the beta feature
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-participant-drop-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Participant Drop lets the primary agent remove an eligible participant from an active Webex Contact Center voice conference. Use the voice task's `dropConferenceParticipant` method, then refresh your application from the updated task rather than removing a participant from the UI immediately.

## Selected section

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

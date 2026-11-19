---
type: Guide
title: Webex Contact Center Web Widgets | Components| Agent Wellness Break Beta
display_title: Agent Wellness Break Beta
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta)

Use this guide to test Agent Wellness Break in the Cisco AI Assistant React widget. The widget shows suggestions and offers, runs the timed break after active work is complete, and returns the agent to Available.

## Before you begin

- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use an approved Contact Center organization and agent.
- Confirm that the organization has an AI Assistant entitlement and that agent wellbeing and wellness break reminders are enabled. The widget uses the effective SDK enablement flag; your application does not need a separate wellness feature toggle.
- Use `@webex/cc-widgets` **1.28.0-next.62** and `@webex/contact-center` **3.12.0-next.133**. Use the `webex` aggregate package **3.12.0-next.220** if your application uses it. Pin these package versions for this beta.
- Use `@momentum-ui/react-collaboration` **26.201.9**. The published Station Login package requires this version. Install the other peer dependencies required by your widget package, including compatible React, React DOM, and `@momentum-ui/web-components` versions.
- Complete the [Webex Contact Center Web Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart). Initialize the shared store once and complete Station Login before testing.
- Use a React host with enough space for the break overlay. An iframe can cover only its own viewport unless its parent supplies an overlay.

Watch the [Widgets wellness demonstration](https://app.vidcast.io/share/c557c146-0941-41a4-ac92-493297d5da83) for an example of the test flow.

## Test with the Widgets sample application

Use the beta React sample build supplied with your invitation. Confirm that it includes the versions listed above. The widget responds to live wellness events; there is no control to create a mock offer.

1. Sign in as the beta test agent and initialize the sample with a temporary developer access token. Do not put the token in a screenshot or test report.
2. Select **AI Assistant**, complete Station Login, and set the agent to **Available**. Before a wellness event, confirm that the assistant shows its landing content.
3. Wait for a wellness suggestion. Select **Take wellbeing break** once. Confirm that the request remains pending until the service approves or denies it. A later suggestion is required before another manual request is available.

    ![Cisco AI Assistant wellness suggestion with the Take wellbeing break button.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltef5b2200cafaef01/6abe90fedb047411f049d8f3/agent-wellness-widgets-suggestion.jpg)

4. Test a direct offer with the assistant open. Confirm that the offer appears in the panel. Repeat with the panel closed or minimized. Confirm that one actionable notification shows **Take a break** and **Later**.

    ![Well-being break scheduled card with Take a break and Later buttons.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75d844166811e26a/6abe907f60418e3b53b9bfcd/agent-wellness-widgets-direct-offer.jpg)

    ![Wellness notification with Later and Take a break actions.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8283cd3fa6763e30/6abe908bfd70711b0db2b411/agent-wellness-widgets-actionable-notification.jpg)

5. Select **Later** and confirm that the agent state does not change. Test an unanswered offer and confirm that it expires after five minutes without changing the state.
6. Accept a direct offer. Confirm that the agent enters `WellbeingBreak`, sees a five-second start countdown, a 60-second break, and a five-second ending countdown, and then returns to **Available**.

    ![Wellness break overlay over the React sample app with a progress indicator.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt430643953ce4a082/6abe908061afb887872409b6/agent-wellness-widgets-break-progress.jpg)

7. Accept while a voice or digital task is active. Confirm that the break waits until the task and required wrap-up finish. During the break, confirm that User State shows the timed `WellbeingBreak` state but does not list it as a selectable idle code.
8. Review wellness history. Select **Clear** and confirm that it removes displayed history without cancelling an active offer or break.
9. Test keyboard focus, reduced motion, and a blocked audio or animation request. Confirm that the break remains usable and still returns the agent to Available.
10. Repeat after logout, a station-session change, a browser refresh during the break, and a connection interruption. Confirm that stale offers do not reappear and that old-session work does not continue.

The test passes when the suggestion and offer actions work, active work delays the timer, and every completed break returns the agent to Available.

## Add the widget to a React application

Keep the shared store and Station Login flow from the Widgets quickstart. Import `AIAssistant` from the existing `@webex/cc-widgets` aggregate. Your application does not need to call the wellness SDK methods when it uses this widget.

```jsx
import {AIAssistant} from '@webex/cc-widgets';

<AIAssistant
  wellnessBreakOverlayTarget="viewport"
  onWellnessBreakOffered={() => recordLifecycle('offered')}
  onWellnessBreakAccepted={() => recordLifecycle('accepted')}
  onWellnessBreakStarted={() => recordLifecycle('started')}
  onWellnessBreakEnded={() => recordLifecycle('ended')}
  onWellnessBreakError={(error) => recordErrorCode(error.code)}
/>
```

The callbacks are optional. `recordLifecycle()` and `recordErrorCode()` represent your application's handlers. Do not record notification text, agent identifiers, or customer data.

`wellnessBreakOverlayTarget` defaults to `"viewport"`. Use `"assistant"` to cover the assistant root, or pass an `HTMLElement` for a custom React host container. The active overlay stays in place if the assistant panel is closed or minimized. If the widget is inside an iframe, viewport coverage stops at the iframe boundary.

The widget supplies its wellness animation and audio. It loads the media when the break needs it. If audio cannot play or animation cannot load, the break continues with a silent or static presentation. You can set `wellnessAudioUrl` if your application uses an approved audio URL.

## Validate the integration

- Before a live suggestion or offer arrives, the widget shows no wellness action. A consumed suggestion is not reused.
- An open assistant shows one offer card. A closed or minimized assistant shows one actionable notification.
- A direct offer changes the agent to `WellbeingBreak` before it sends `ACCEPTED`. **Later** sends `REJECTED`; an unanswered offer sends `NO_RESPONSE` once.
- An approved manual request starts the break without a second `ACCEPTED` action.
- Active tasks and required wrap-up finish before the timed break starts. Completion returns the agent to Available with aux code `0`.
- The overlay traps focus during the break, Escape does not dismiss it, and focus returns after completion. Reduced motion uses a static treatment.
- A media failure does not block Available restoration. Logout, session changes, and unmount stop work for the old session.

## Troubleshoot the test

- **No suggestion or offer appears:** Check the organization settings, package versions, Station Login, effective wellness enablement, and AI Assistant real-time connection. The widget needs a live backend event.
- **A suggestion is hidden:** Check whether active Real Time Assist content has priority in the assistant panel.
- **The offer appears in an unexpected place:** Check whether the panel is open, closed, or minimized. Set `wellnessBreakOverlayTarget` for the host layout you use.
- **The break has not started:** Check for an active task or required wrap-up. The timer starts only after the agent enters the wellness state and work is safe.
- **The overlay does not cover the full app:** Check the target element and any iframe boundary. A child iframe cannot cover its parent page by itself.
- **The UI looks incomplete:** Check that the application uses `@momentum-ui/react-collaboration` 26.201.9 and the package peer dependencies.

## Share feedback

Use the feedback channel supplied with your beta invitation. Include the test time and time zone, package versions, browser, host layout, lifecycle phase, expected result, actual result, and a non-sensitive error code. Do not include access tokens, agent names, notification text, or customer content.

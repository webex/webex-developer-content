---
type: Guide
title: Webex Contact Center Web Widgets | Components | Participant Drop in Webex Contact Center Widgets (Beta)
display_title: Participant Drop in Webex Contact Center Widgets (Beta)
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta)

Use the existing CallControlCAD widget to remove an eligible participant from an active conference. The Participants menu shows who is on the call, while the current primary agent can use Drop where permitted. This beta guide covers both the React widget and its Web Component wrapper.

## Before you begin

Follow the [Contact Center Widgets quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart) to initialize the store, sign in, and render CallControlCAD. Use a beta-enabled Contact Center organization and compatible Widgets and Contact Center SDK builds supplied for your evaluation. Confirm the agent has an active voice conference and that your backend permits participant removal.

Participant Drop is part of **CallControlCAD** and `<widget-cc-call-control-cad>`. It adds no Drop-specific prop, Web Component attribute, or feature flag. The standard CallControl widget does not show this roster.

## Use the existing widget

In a React integration, render the existing component after your normal store and agent setup:

```tsx
import {CallControlCAD} from '@webex/cc-widgets';

<CallControlCAD />;
```

For a Web Component integration, register the components through the existing package entry point, initialize the store as described in the [Widgets quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart), and render the existing element:

```ts
import {store} from '@webex/cc-widgets/wc';

// Complete your normal store.init(...) and agent sign-in before rendering.
const callControl = document.createElement('widget-cc-call-control-cad');
document.body.appendChild(callControl);
```

No Participant Drop switch is needed. See the [CallControlCAD component guide](https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad) for general integration details.

In the React sample, select **Call Controls with Call Associated Data (CAD)** before initializing the widgets.

![React Widgets sample with Call Controls with Call Associated Data (CAD) selected in the widget list.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt32019217202a0258/6ac3841f517fb6cd17971e03/participant-drop-widgets-cad-setup.png)

*React sample setup. The selected CAD widget provides the participant menu shown below.*

## What agents should see

- **Primary agent:** The Participants menu can show the Customer and other supported call participants. Drop is available for eligible Customer, Agent, and joined Entry Point/dial-number (EP-DN) rows. Dropping the Customer requires confirmation; eligible Agent and joined EP-DN rows act immediately.
- **Other agents:** The roster remains visible where eligible, but Drop actions are hidden. Supervisor rows are visible without a Drop action. The primary-agent label and icon follow the call owner reported by Contact Center; the widget does not choose a successor.
- **Before an EP-DN consult joins:** The dialed number may appear in the list while the call is ringing. Its Drop action stays disabled until it becomes a conference participant. An active, non-held consult disables other Drop actions; a held consult can leave established conference targets enabled.
- **While Drop is pending:** All Drop actions are locked until the request completes. The list changes when Contact Center reports the participant leaving, not when the button is first clicked. A failed request shows a generic error. Hosts can register the existing store-level error handler with `store.setOnError((widgetName, error) => { /* handle the error */ })`; the callback receives the widget name and an `Error`. Avoid logging participant identifiers or raw event payloads.
- **As the call changes:** A Customer-only, one-to-one call uses the original call UI. If the Customer leaves but another supported participant remains with the viewing agent, the Participants section stays visible. If the last other participant leaves and only the Customer remains, the roster closes.

The cropped views below show the same menu for the primary agent and a secondary agent. Identifying details are redacted.

![Primary agent participant menu showing Customer and Participants sections with Drop actions; identifying details are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte73fe49ce0e42a71/6ac384469c578226f1d674d8/participant-drop-widgets-primary-menu.png)

*Primary-agent view: eligible Customer and Agent rows have Drop actions.*

![Secondary agent participant menu showing Customer and Participants sections and a Primary marker, without Drop actions; identifying details are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2a5431a7defaa22b/6ac384999c57821128d6751f/participant-drop-widgets-secondary-menu.png)

*Secondary-agent view: the current owner is marked Primary, and this agent has no Drop actions.*

The backend remains responsible for authorizing and removing participants. Visibility of a Drop button is not an authorization guarantee.

## Test the beta feature

Test with agents who can join the same voice conference. For each case, note whether you are the primary or a secondary agent and whether a consult is ringing, connected, or held.

| Scenario | Action | Expected result |
| --- | --- | --- |
| Primary and secondary views | Open Participants on both agents' screens. | Both see eligible rows. Only the current primary agent sees enabled Drop actions. |
| Agent Drop | From the primary agent's screen, drop another joined Agent. | The request shows a pending state. After the participant-left update, that Agent disappears; the remaining call stays usable. |
| Customer confirmation | Select Drop for Customer, then Cancel or press Escape. Repeat and confirm. | Cancel/Escape makes no Drop request. Confirm starts Drop, and the Customer row disappears after the reported update. |
| Customer leaves with another Agent present | Have the Customer hang up or be dropped. | Customer disappears; Participants remains for the other Agent. |
| Return to one-to-one | Remove the last other Agent while the Customer remains. | The Participants menu disappears and the original one-to-one call UI remains. |
| EP-DN consult | Dial an Entry Point and observe it before and after a participant answers and joins. | The dialed number can appear before merge with Drop disabled; the joined participant is shown without a duplicate stale EP-DN row. |
| Consult gating | Start a consult, then hold or end it. | An active, non-held consult blocks Drop; eligible established targets become available when the consult is held or ends. |
| Primary agent changes | Have the primary agent leave while two other agents remain. | The new owner receives Drop permission; other agents see the new Primary label and icon after owner-change updates. |
| Nested consult cleanup | While Agent 2 consults Agent 3, have the primary agent drop Agent 2. Repeat while Agent 3 is ringing and after answer. | Check that Agent 2's call UI closes and Agent 3's consult ends. If either remains visible, report the event sequence and timing; do not assume the local button can end another agent's task by itself. |

For a walkthrough, see the [Participant Drop widget sample video](https://app.vidcast.io/share/f5acb405-3a94-459a-93d8-ce931eb20f53). You can also use the [hosted React sample](https://widgets.webex.com/samples-cc-react-app/index.html) if it has the approved beta build.

## Troubleshooting and feedback

- **Drop is absent or disabled:** Check the current owner, call membership, consult state, and whether the target has joined. Customer-only calls do not show the conference roster; Supervisor rows are view-only.
- **Names or confirmation are missing:** Confirm the Widgets and Momentum Design component versions supplied for this beta are installed together. If a dialog fails to open, capture the sanitized browser error and version list; do not repeatedly click Drop.
- **Primary status or a dropped call looks stale:** Record which agent saw the issue, the event names and approximate timestamps, and whether a refresh changed the result. Avoid sharing raw routing payloads.
- **Drop fails:** The generic message does not identify the server-side reason. Check authorized backend diagnostics through your normal support process.

When reporting a result, send the scenario, React or Web Component integration mode, package versions, browser/OS, participant type, primary/secondary role, call direction, consult state, expected versus actual behavior, and sanitized console stack or routing event names/timestamps. **Do not send access tokens, names, phone numbers, ANI/DNIS, headers, request URLs, or raw event payloads.**

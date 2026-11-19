---
type: Guide
title: Webex Contact Center Web Widgets | Components | Webex Better Together Widgets Beta
display_title: Webex Better Together Widgets Beta
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta)

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Before you begin

- Complete the [Webex Contact Center Web Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart), including widget initialization, authentication, and station login.
- Use a Contact Center organization provisioned for Webex Together / wxApp telephony.
- Sign in using an **Extension** or **Agent DN** station login. Browser/WebRTC-only login is not the supported answer path.
- Run Webex App desktop version 44.12 or later on the same computer as the embedded application and sign in as the same user.
- Use React 18.3.1 or later for a React host.
- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use the beta feedback channel shared with your invitation.

The Contact Center SDK handles Webex App telephony routing and mute synchronization. The widgets are the UI layer; no new widget export is required. This release uses the existing `IncomingTask`, `TaskList`, and `CallControl` widgets.

## Install the beta Widgets package

Use `@webex/cc-widgets` version `1.28.0-next.60` or later from this beta train. For a widgets-only host, install the Widgets package; use a matching SDK and Widgets release set when managing both dependencies directly.

```bash
npm install @webex/cc-widgets@1.28.0-next.60
```

Or with Yarn:

```bash
yarn add @webex/cc-widgets@1.28.0-next.60
```

## Enable the feature before initialization

Set `webexConfig.cc.enableWxBetterTogether` before calling `store.init()`. The setting defaults to `false` and is initialization-only in this release.

```js
import { store } from '@webex/cc-widgets';

const webexConfig = {
  cc: {
    enableWxBetterTogether: true,
  },
};

await store.init({ webexConfig, access_token: accessToken });
```

If your host initializes a Webex instance separately, set the same Contact Center configuration before initializing that instance and then initialize the widgets with it. The feature is not gated by a Contact Center user or organization feature toggle.

## Test with the Widgets sample app

Use the Contact Center Widgets sample app from the Widgets repository and keep Webex App desktop open on the same computer, signed in as the test agent.

1. Open the sample app and authenticate as the test agent.
2. Before initializing widgets, enable **Answer on Webex** in **SDK Toggles**. This sets `webexConfig.cc.enableWxBetterTogether`.

   ![SDK Toggles with Answer on Webex enabled](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7442abce6c38419d/6abe423bfcb9ad705c2b14d9/webex-better-together-widgets-setup.png)
3. Initialize the widgets and confirm there are no errors.
4. Select `IncomingTask`, `TaskList`, and `CallControl` in the widget picker.
5. Log in with an Extension or Agent DN and set the agent state to Available.
6. Start an inbound wxApp voice interaction. Confirm the offer displays **Accept** and **Decline** in `IncomingTask` or `TaskList`.

   ![Incoming task card with Accept and Decline actions](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1ebe47578b88682d/6abe43248aebed7ab2dca83b/webex-better-together-widgets-incoming-task.png)
7. Accept the task and confirm the call engages in Webex App desktop.
8. Confirm `CallControl` displays **Mute** and **Keypad** during the engaged call.

   ![Call controls showing Mute and Keypad during an active call](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt088dd865a202ee3f/6abe43c0ec9eb7e00569d3d4/webex-better-together-widgets-call-control.png)
9. Mute in the embed and confirm the Webex App microphone state matches. Optionally mute or unmute in Webex App and confirm the embed updates.

   ![Mute control reflecting the synchronized call mute state](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7c75e525a4a36f19/6abe445bfc9e37d19428c78c/webex-better-together-widgets-mute-control.png)
10. Send keypad digits and confirm the IVR receives the tones.

   ![Dialpad and DTMF controls displayed during an active call](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6ca148cfd9c16523/6abe455ef5361482690df19c/webex-better-together-widgets-dialpad.png)
11. End and wrap up the active task, then set the agent state to Available. Start a fresh inbound wxApp voice interaction and, while its offer is pending, cause an Accept or Decline failure, such as by making Webex App unavailable. Confirm an inline error appears on the offer card. Restore Webex App and accept the pending offer before continuing to step 12.

   ![Incoming task card showing the unable-to-answer error and retry message](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3e638f63e20b8b08/6abe45a8e2bfa6b505f4d590/webex-better-together-widgets-error-state.png)
12. End the task and confirm the offer state clears.

## Integrate with a host application

The feature uses existing widget exports. Enable the feature before initialization, then render the normal IncomingTask, TaskList, and CallControl widgets in the host’s layout. The SDK updates control visibility and enabled state according to the task and login type.

- **Incoming offers:** Accept and Decline are available for supported wxApp voice offers. `IncomingTask` resolves the live task from `store.taskList` by `interactionId`, so the Accept control stays current when SDK controls update. Pass the store-provided `incomingTask` prop.
- **Offer errors:** If accept or decline fails, the offer card shows an inline error. The shared `offerActionErrors` map is keyed by `interactionId`, keeping `TaskList` and `IncomingTask` consistent for the same interaction.
- **Mute:** `CallControl` exposes Mute for an engaged wxApp call when the flag is enabled. The widget passes explicit intent to `task.toggleMute({ muted })`; mute changes made in Webex App update the embedded control through the SDK event `task:wxapp-mute-state-updated` and the store’s `isMuted` state.
- **Keypad:** `CallControl` exposes Keypad under the same engaged-call condition. It sends digits with `task.transmitDtmf({ dtmf })`. The widget keypad accepts `0`–`9`, `*`, and `#`; commas and other characters are discarded.
- **Other call actions:** Hold, resume, transfer, consult, conference, end, wrap-up, and recording continue to use their existing SDK and widget paths.

## Release scope and limitations

This beta supports Accept and Decline on Webex App voice offers, bidirectional Mute synchronization, in-call DTMF, toast suppression when enabled, and Extension or Agent DN station login.

The following are not supported in this release:

- Hold-state synchronization with Webex App. Existing hold and resume actions may not match the Webex App state.
- Browser/WebRTC station login as the Webex Better Together answer path.
- Webex App on mobile or tablet as the primary answer client.
- Full removal of the Webex mini call window.
- Changing `enableWxBetterTogether` after initialization.

Only one client should answer a given offer. `allowMultiLogin: true` is supported, but `allowMultiLogin: false` is recommended for a single CRM embed session per agent.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Accept, Mute, or Keypad is missing | Set `enableWxBetterTogether: true` before initialization, then initialize and log in again. |
| Accept remains disabled | Confirm the host passes the store-provided task through the `incomingTask` prop. `IncomingTask` resolves the current task from `store.taskList` by `interactionId`; use a Widgets release that includes this live task resolution behavior. |
| Mute is out of sync | Confirm the call is an engaged wxApp call, Webex App is running, both clients use the same user on the same computer, and the agent used Extension or Agent DN login. Log out and back in if needed. |
| Accept or Decline shows an inline error | Confirm Webex App is signed in and reachable and the organization is provisioned for wxApp offers. |
| A native Webex incoming toast still appears | Confirm the flag was enabled before initialization and station login completed after initialization; log out and back in. |
| Toast suppression remains stale after an embed crash | Log out and back in. Reinitialize with the flag off to clear suppression on the next login. |
| The feature works in the sample but not in production | Deploy matching `@webex/contact-center` and `@webex/cc-widgets` releases that include Webex Better Together support. |

## Beta feedback

Please share setup, rendering, telephony, mute synchronization, and DTMF feedback through the beta channel shared with your invitation. Include whether the issue occurred in the Widgets sample app, a React host app, or a Web Component host app.

- How easy was setup and testing on a scale of 1 to 5?
- Did Accept and Decline work reliably from `IncomingTask` and `TaskList`?
- Did bidirectional mute synchronization work as expected?
- Did DTMF work as expected for IVR entry?
- Did `CallControl` render Mute and Keypad correctly in the host layout?
- What issues did you encounter?

## Related documentation

- [Webex Contact Center Web Widgets Introduction](https://developer.webex.com/docs/cc-web-widgets-introduction)
- [Webex Contact Center Web Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart)
- [Webex Contact Center SDK Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks)

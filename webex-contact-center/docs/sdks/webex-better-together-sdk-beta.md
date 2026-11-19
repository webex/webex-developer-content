---
type: Guide
title: Webex Contact Center Web SDK | Webex Better Together SDK Beta
display_title: Webex Better Together SDK Beta
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta)

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Overview and limitations

| Host application | Contact Center SDK | Voice client |
| --- | --- | --- |
| CRM, such as Salesforce or ServiceNow, or a custom web app | `@webex/contact-center` | Webex App desktop on the same computer, signed in as the same user |

Agents use the host application to accept or decline offers, mute or unmute an engaged call, and send keypad digits. The voice call runs in Webex App.

**Limitations for this beta:**

- Webex App hold-state synchronization is deferred; existing hold/resume controls may not match Webex App state.
- Browser/WebRTC-only station login and mobile/tablet Webex App are outside this answer flow.
- The SDK initialization flag is init-only. Changing it requires reinitializing the SDK.

For existing hold, transfer, consult, end, wrap-up, and WebRTC controls, see [Webex Contact Center SDK Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks).

## Before you begin

- Complete the [Webex Contact Center SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication) setup.
- Use a Contact Center organization provisioned for Webex Together / wxApp telephony. Confirm with your Cisco contact that the organization's Webex-side notification settings are enabled.
- Sign in to the Contact Center station using an **Extension** or **Agent DN**. Browser/WebRTC-only station login is not supported for this answer flow.
- Run Webex App desktop version 44.12 or later on the same computer as the host application, signed in as the same user.
- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use the beta feedback channel shared with your invitation.

Webex Better Together is not gated by a Contact Center user or organization feature toggle. The `enableWxBetterTogether` setting is a separate SDK initialization flag, defaults to `false`, and must be set to the boolean value `true` before SDK initialization, registration, and station login.

## Install the beta SDK

Use `@webex/contact-center@3.12.0-next.131` for this beta guide. Pin the package version so an unpinned install does not select a different build.

```bash
npm install @webex/contact-center@3.12.0-next.131
```

Or with Yarn:

```bash
yarn add @webex/contact-center@3.12.0-next.131
```

## Enable Webex Better Together before initialization

Use an access token for the same user who is signed in to Webex App: an OAuth user token for an integration or a Personal Access Token (PAT) for testing. For OAuth integrations, request `spark:calls_write` for call controls and `spark:calls_read` for mute-state read-back, in addition to the Contact Center scopes. Reauthorize the user after adding these scopes to an existing integration. Bot tokens are not supported for this flow.

Import the SDK and set the flag in the options passed to `Webex.init()`. Obtain `token` through the [Authentication guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication).

```js
import Webex from '@webex/contact-center';

const webex = Webex.init({
  credentials: {
    access_token: token,
  },
  config: {
    cc: {
      enableWxBetterTogether: true,
      allowMultiLogin: false,
    },
  },
});

// Capture readiness immediately after initialization.
const sdkReady = new Promise((resolve) => webex.once('ready', resolve));
```

Wait for the SDK's `ready` event before registering, then complete station login with your assigned team and Extension or Agent DN. Replace the example values below with your agent's configuration.

```js
await sdkReady;
await webex.cc.register();
await webex.cc.stationLogin({
  teamId: '<TEAM_ID>',
  loginOption: 'EXTENSION', // Use 'AGENT_DN' for an Agent DN login.
  dialNumber: '<EXTENSION_OR_DN>',
});
```

Only one client should answer a given offer. `allowMultiLogin: true` is supported, but `allowMultiLogin: false` is recommended for a single CRM embed session per agent. See the [Quickstart guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication) for the full initialization, login, and agent-state flow.

## API and event reference

### Configuration and task methods

| Configuration or method | Purpose |
| --- | --- |
| `config.cc.enableWxBetterTogether` | Enable the flow before SDK initialization and station login. |
| `task.accept()` | Accept an offered Webex App voice task. |
| `task.decline()` | Decline an inbound offer or cancel an outbound ringing offer. |
| `task.toggleMute({ muted })` | Set the intended Webex App mute state on an engaged call. |
| `task.getWxAppMuted()` | Read the SDK-cached mute state. |
| `task.syncWxAppMuteFromCallDetails()` | Asynchronously refresh mute state from call details. |
| `task.transmitDtmf({ dtmf })` | Send in-call keypad digits. |

### Events

| Subscribe on | Event | Host action |
| --- | --- | --- |
| `webex.cc` | `task:incoming` | Add the offered task to the UI and attach its control listener. |
| `webex.cc` | `task:hydrate` | Restore task bindings after reload or reconnect. |
| `task` | `task:ui-controls-updated` | Refresh control visibility and enabled state. |
| `task` | `task:assigned` | Attach mute synchronization and seed mute state when the task becomes the active engaged call. |
| `task` | `task:rejected` | Clear an offer that is rejected or goes unanswered. |
| `task` | `task:wxapp-mute-state-updated` | Update the mute icon from the `{ muted }` payload. |
| `task` | `task:end` | Detach listeners when the task ends. |

## Add task controls to your host application

Use each `task.uiControls.main` entry independently: `isVisible` decides whether a control appears, and `isEnabled` decides whether its action can be used. A visible control with `isEnabled: false` stays visible but disabled. Recheck `isEnabled` in the click handler.

Listen for incoming and hydrated tasks, and register each task listener inside its callback or a helper that receives that task:

```js
const watchedTasks = new WeakSet();

function watchTask(task) {
  if (watchedTasks.has(task)) return;
  watchedTasks.add(task);

  const updateControls = () => {
    // Render from isVisible; set disabled from !isEnabled.
  };
  task.on('task:ui-controls-updated', updateControls);
  task.once('task:end', () => {
    task.off('task:ui-controls-updated', updateControls);
    watchedTasks.delete(task);
  });
}

webex.cc.on('task:incoming', (task) => {
  // Add the offer to the host application's UI.
  watchTask(task);
});

webex.cc.on('task:hydrate', (task) => {
  // Restore task bindings after reload or reconnect.
  watchTask(task);
});
```

The handlers below receive host callbacks: `showError` displays an actionable error to the agent, and `updateMuteIcon` renders a boolean mute state. Catch SDK/telephony failures in the host UI so the agent can check Webex App and retry an action while it is still available.

### Accept and decline an offer

Render **Accept** and **Decline** from their respective `isVisible` values, and disable each button when its `isEnabled` value is false.

```js
async function onAccept(task, showError) {
  if (!task.uiControls?.main?.accept?.isEnabled) return;
  try {
    await task.accept();
  } catch (error) {
    showError(error);
  }
}

async function onDecline(task, showError) {
  if (!task.uiControls?.main?.decline?.isEnabled) return;
  try {
    await task.decline();
  } catch (error) {
    showError(error);
  }
}
```

For an outbound ringing offer, `decline()` cancels the offer; it is not the same as calling `reject()`. The SDK emits `task:assigned` after acceptance and `task:rejected` when a task is rejected or goes unanswered. Refresh offer controls on `task:ui-controls-updated`.

### Mute and synchronize mute state

Render **Mute** from `task.uiControls.main.mute.isVisible`, and disable it when `isEnabled` is false. Always pass the intended mute state, and await each call:

```js
async function onMuteClick(task, uiShowsMuted, showError) {
  if (!task.uiControls?.main?.mute?.isEnabled) return;
  try {
    await task.toggleMute({ muted: !uiShowsMuted });
  } catch (error) {
    showError(error);
  }
}
```

Attach the Webex App mute listener when the task becomes the active engaged call, such as after `task:assigned`. The callback receives `{ muted }`:

```js
function attachWxAppMuteSync(task, updateMuteIcon) {
  const onSync = ({ muted }) => updateMuteIcon(muted);
  const detach = () => {
    task.off('task:wxapp-mute-state-updated', onSync);
    task.off('task:end', detach);
  };

  task.on('task:wxapp-mute-state-updated', onSync);
  task.once('task:end', detach);
  return detach;
}
```

Keep the returned `detach` callback and invoke it before replacing or removing the active task in the host UI. Avoid attaching duplicate listeners to the same task.

After engaging, reconnecting, reloading, or switching the active task, await mute backfill before reading cached state:

```js
async function seedMuteState(task, updateMuteIcon, showError) {
  try {
    const syncedMuted = await task.syncWxAppMuteFromCallDetails();
    if (typeof syncedMuted !== 'boolean') {
      showError('Mute state could not be refreshed. Check Webex App and retry.');
      return;
    }
    updateMuteIcon(task.getWxAppMuted());
  } catch (error) {
    showError(error);
  }
}
```

For a hydrated engaged call, restore the listener and seed mute state even if the host did not observe the original acceptance event.

### Send keypad digits

Render **Keypad** from `task.uiControls.main.keypad.isVisible`, and disable it when `isEnabled` is false. Send in-call digits using `transmitDtmf()`:

```js
async function onKeypadDigits(task, dtmf, showError) {
  if (!task.uiControls?.main?.keypad?.isEnabled) return;
  try {
    await task.transmitDtmf({ dtmf });
  } catch (error) {
    showError(error);
  }
}
```

Supported values are `0`–`9`, `*`, and `#`; a comma adds a one-second pause between tones.

## Test the feature

Keep Webex App desktop open on the same computer as the host application and use an organization provisioned for wxApp telephony.

[Watch the SDK sample walkthrough — Answer, Mute, and Keypad (Vidcast, 4m 33s)](https://app.vidcast.io/share/02dd6537-fb8c-4604-b9d1-ef6816f91803)

### Test with the SDK sample app

Use the [Webex Contact Center SDK sample app](https://webex.github.io/webex-js-sdk/samples/contact-center/) to register, log in with an Extension or Agent DN, and set the agent to Available.

1. Start an inbound Webex App voice offer and confirm **Accept** and **Decline** appear.
2. Accept the offer and confirm the call engages in Webex App.
3. Mute in the sample app and confirm the Webex App microphone mutes. Unmute in Webex App and confirm the host mute icon updates.
4. Refresh during the engaged call and confirm mute state is restored from call details.
5. Send keypad digits and confirm they reach the IVR.
6. After ending and wrapping up the active task, create an outbound ringing offer and confirm **Decline** clears it.

### Test with your host application

1. Initialize with `enableWxBetterTogether: true`, await SDK readiness, then register and complete Extension or Agent DN station login.
2. Bind incoming and hydrated tasks to the host UI and refresh controls on `task:ui-controls-updated`.
3. Wire guarded Accept/Decline handlers to the offered task.
4. When the task becomes the active engaged call, attach its mute listener and seed mute state. Wire Mute and Keypad to that task.
5. Set the agent to Available, create an inbound offer, and verify acceptance, mute in both directions, keypad entry, and refresh/reconnect recovery.
6. End and wrap up using the existing task methods. Confirm host listeners are detached on task end or host removal, and only one client answers each offer.

For existing hold, transfer, consult, end, and wrap-up behavior, follow [Webex Contact Center SDK Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks).

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Accept, Mute, or Keypad is missing | Reinitialize with `enableWxBetterTogether: true`, then register and log in again. |
| Accept remains disabled | Refresh the task from the SDK task manager and listen for `task:ui-controls-updated`; keep a visible disabled button rendered. |
| Mute is out of sync | Confirm an engaged wxApp call, Webex App running, the same user and computer, and Extension or Agent DN login. Await mute backfill; log out and back in if needed. |
| Accept, Decline, Mute, or Keypad reports an error | Display the error in the host UI. Check Webex App connectivity and organization provisioning; retry only while the control is enabled. |
| A native Webex incoming toast still appears | Confirm the flag was enabled before initialization and station login completed after initialization; log out and back in. |
| The feature works in the sample but not in the host app | Confirm the host uses `@webex/contact-center@3.12.0-next.131` and the same initialization and station-login flow. |

## Beta feedback

Please share setup, API, mute synchronization, DTMF, and telephony feedback through the beta channel shared with your invitation. Include whether the issue occurred in the SDK sample app or a custom host application.

- How easy was setup and testing on a scale of 1 to 5?
- Were `accept()`, `decline()`, `toggleMute({ muted })`, and `transmitDtmf({ dtmf })` clear enough to build the host UI?
- Did bidirectional mute synchronization and refresh recovery work as expected?
- Did DTMF work as expected for IVR entry?
- What issues did you encounter?

## Related documentation

- [Webex Contact Center SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart)
- [Webex Contact Center SDK Authentication](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication)
- [Webex Contact Center SDK Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks)

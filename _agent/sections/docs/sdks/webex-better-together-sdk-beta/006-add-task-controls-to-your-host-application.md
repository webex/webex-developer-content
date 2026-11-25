---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add task controls to your host application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md) [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

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

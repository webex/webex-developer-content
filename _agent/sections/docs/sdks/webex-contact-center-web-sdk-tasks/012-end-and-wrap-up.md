---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- End and Wrap-up
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-tasks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This page documents how to work with tasks using only public SDK methods and events.

---



> **Info**
>
> It is necessary to listen to all task events only if your application supports multi-session usage (i.e., the same agent is signed in from multiple tabs, windows, or devices). For single-session applications, promise-based method responses are sufficient for most scenarios, and you typically only need to subscribe to a select set of events. The specific events required are indicated in the relevant sections below.

## Selected section

## End and Wrap-up

### End Task

End the active task.

```javascript
await currentTask.end();
```

#### Request Parameters
No parameters.

#### Response Payload

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

#### Relevant Task Events

- `task:end` — Includes `wrapUpRequired` in `task.data` to indicate wrap-up necessity.



> **Info**
>
> Subscribe to `task:end` to determine wrap-up behavior. The event payload includes fields such as `wrapUpRequired` (when configured). Without this event, your app may not know when to present the wrap-up.



### Automatic Wrap-up Timer

Some deployments configure an automatic wrap-up timer. When present, the SDK exposes this via `task.autoWrapup` after a task ends with wrap-up required.

- `task.autoWrapup.isRunning()` — Returns whether the timer is currently active.
- `task.autoWrapup.getTimeLeftSeconds()` — Returns remaining seconds before auto wrap-up completes.

Recommended usage (listen to `task:end` and show a countdown when available):

```javascript
webex.cc.on('task:end', (task) => {
  if (!task.data?.wrapUpRequired) return;

  const autoWrap = task.autoWrapup;
  if (autoWrap?.isRunning()) {
    const autoWrapupInterval = setInterval(() => {
      // Add UI logic inside the interval
  }, 1000);
  }
});
```

If you manage task state via selection/hydration, you can also check `currentTask.data.wrapUpRequired` and `currentTask.autoWrapup` in your UI update routine to start/stop the timer when entering wrap-up.

### Wrap-up Task

Submit wrap-up details and complete the task.

```javascript
await currentTask.wrapup({ wrapUpReason: '<REASON>', auxCodeId: '<CODE_ID>' });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `auxCodeId` | string | yes | Required wrap-up code id. |
| `wrapUpReason` | string | yes | Required human-readable wrap-up reason. |

#### Response Payload

- Resolves with a TaskResponse.

#### Relevant Task Events

- `task:wrappedup`

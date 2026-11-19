---
type: Guide
title: Webex Contact Center Web SDK | Tasks
display_title: Tasks
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks)

This page documents how to work with tasks using only public SDK methods and events.

---



> **Info**
>
> It is necessary to listen to all task events only if your application supports multi-session usage (i.e., the same agent is signed in from multiple tabs, windows, or devices). For single-session applications, promise-based method responses are sufficient for most scenarios, and you typically only need to subscribe to a select set of events. The specific events required are indicated in the relevant sections below.



## Overview

Tasks represent customer interactions. Your app typically:
- Listens for new and existing tasks
- Renders a task list and a selected task view
- Accepts or declines inbound tasks
- Performs channel-appropriate controls (e.g., telephony call controls)
- Transfers or consults when supported
- Ends and wraps up tasks
- Initiates outbound calls (telephony)

## Receiving Tasks

Subscribe to task events from the plugin:

```javascript
// New inbound tasks
webex.cc.on('task:incoming', (task) => {
  // Add task to your UI and set currentTask
});

// Existing/updated tasks
webex.cc.on('task:hydrate', (task) => {
  // Refresh UI for updated task data
});

// Optional: render task list
const taskList = webex.cc.taskManager.getAllTasks();
```

## Selecting and Handling a Task

When a task is selected, update the UI and enable/disable controls based on the channel and state. For example, telephony tasks expose voice controls, while digital tasks do not.


## Response Type: TaskResponse

All task operations resolve to a common response union type:

| variant | description |
| --- | --- |
| `AgentContact` | Structured contact update payload containing task/interaction data (e.g., `trackingId`, `agentId`, `mediaResourceId`, `interaction`, `consultMediaResourceId`, `destAgentId`, etc.). |
| `Error` | Error object when an operation fails. |
| `void` | No payload for operations that do not return data. |

Use per-method sections below to see whether a given call typically returns a payload or `void`.

### AgentContact payload structure

When a task method resolves with an `AgentContact`, common fields include:

| key | description |
| --- | --- |
| `interactionId` | Unique identifier for the interaction. |
| `trackingId` | Tracking identifier for diagnostics/telemetry. |
| `agentId` | Current agent id. |
| `mediaResourceId` | Media resource id for the active leg. |
| `destAgentId` | Destination agent id (consult/transfer scenarios). |
| `consultMediaResourceId` | Media resource id used during consult. |
| `interaction` | Full interaction object (see next section). |
| `reason` / `reasonCode` | Reason details when present (e.g., rejections). |

### Interaction structure

Top-level fields on the `interaction` object (core subset):

| key | description |
| --- | --- |
| `interactionId` | Unique interaction id. |
| `mediaType` | Channel type (e.g., `telephony`, `chat`, `email`, `social`). |
| `state` | Current interaction state. |
| `participants` | Participants map/object. |
| `mainInteractionId` | Main interaction id (optional). |
| `media` | Map of media entries keyed by id (see Media entry). |
| `callProcessingDetails` | Selected call-processing fields (see below). |

Media entry structure (core subset):

| key | description |
| --- | --- |
| `mediaResourceId` | Media resource id. |
| `mediaType` | Media channel type. |
| `isHold` | Whether media is held. |

callProcessingDetails (core subset):

| key | description |
| --- | --- |
| `QMgrName` | Queue Manager name. |
| `virtualTeamName` | Virtual team name. |
| `customerName` | Customer’s name. |
| `ani` / `dnis` | Caller and dialed numbers (where applicable). |
| `pauseResumeEnabled` | Whether pause/resume is enabled (optional). |
| `isPaused` | Whether interaction is paused (optional). |
| `ronaTimeout` | RONA timeout (seconds). |

## Accept Task

Accept an offered task.

```javascript
await currentTask.accept();
```

#### Request Parameters
No parameters.

#### Response Payload

- Telephony (BROWSER): resolves with no payload.
- Digital (chat, email, social): resolves with a [TaskResponse](#taskresponse) object (includes at least `trackingId`).

#### Relevant Task Events

- `task:assigned` — Emitted when the task has been successfully accepted.
- `task:media` — Emitted for telephony tasks with a remote audio track.

## Decline Task

Decline an offered task.

```javascript
await currentTask.decline();
```

#### Request Parameters

No parameters.

#### Response Payload

- Resolves with no payload.

#### Relevant Task Events

- `task:rejected` — Emitted with a reason when a task is rejected/unanswered.

## Voice Media (Telephony)

For telephony tasks, attach remote audio when media is available:

```javascript
currentTask.on('task:media', (track) => {
  const audioElement = document.getElementById('remote-audio');
  audioElement.srcObject = new MediaStream([track]);
});
```

## Real-time Transcriptions

If real-time transcriptions are enabled for the agent profile, the SDK automatically starts and stops transcript streaming as the task moves through supported telephony states. Your application only needs to subscribe to transcript events and render the payload.

```javascript
currentTask.on('REAL_TIME_TRANSCRIPTION', (payload) => {
  const transcript = payload?.data;

  console.log({
    content: transcript?.content,
    isFinal: transcript?.isFinal,
    messageId: transcript?.messageId,
    role: transcript?.role,
    publishTimestamp: transcript?.publishTimestamp,
  });
});
```

#### Relevant Task Events

- `REAL_TIME_TRANSCRIPTION` — Emitted when a real-time transcript chunk is received for the current interaction.

#### Relevant Payload Fields

The `REAL_TIME_TRANSCRIPTION` payload commonly includes these fields:

| key | description |
| --- | --- |
| `content` | Transcript text for the current utterance chunk. |
| `isFinal` | Indicates whether the transcript chunk is final or interim. |
| `messageId` | Unique identifier for the transcript chunk. |
| `role` | Speaker role, such as `AGENT` or `CALLER`. |
| `publishTimestamp` | Publish time in epoch milliseconds. |

#### Fetch Historic Transcripts

Use the public AI Assistant helper to load transcript history for the current interaction:

```javascript
const history = await webex.cc.apiAIAssistant.fetchHistoricTranscripts(
  currentTask.data.agentId,
  currentTask.data.interactionId
);

console.log(history.data);
```



> **Info**
>
> `fetchHistoricTranscripts()` is available only when `aiFeature.realtimeTranscripts.enable` is turned on for the agent configuration.



## Telephony Controls

Use these controls only for telephony tasks.

### Hold Task

Place the active task on hold.

```javascript
await currentTask.hold();
```

#### Request Parameters

No parameters.

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

#### Relevant Task Events

- `task:hold` — Emitted when the task is placed on hold.

### Resume Task

Resume the active task that is held.

```javascript
await currentTask.resume();
```

#### Request Parameters

No parameters.

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

#### Relevant Task Events

- `task:resume` — Emitted when the task is resumed from hold.

### Mute/Unmute (WebRTC)

Toggle the agent’s microphone for Desktop (WebRTC) calls.

```javascript
await currentTask.toggleMute();
```

#### Request Parameters
No parameters.

#### Response Payload

- Resolves with no payload.

### Pause Recording

Pause call recording when permitted. Users must have permission to control the recordings, else this method will fail.

```javascript
await currentTask.pauseRecording();
```

#### Request Parameters
No parameters.

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

#### Relevant Task Events

- `task:recordingPaused`
- `task:recordingPauseFailed`

### Resume Recording

Resume call recording, if it has been paused

```javascript
await currentTask.resumeRecording({ autoResumed: false });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `autoResumed` | boolean | no | Set by caller to indicate automatic resume. Defaults to `false`. |

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

#### Relevant Task Events

- `task:recordingResumed`
- `task:recordingResumeFailed`

## Transfer (All Channels Where Supported)

Transfer the active task to an agent, queue or a PSTN number:

```javascript
await currentTask.transfer({ to: '<DEST_ID>', destinationType: 'agent' /* or 'queue' or 'dialNumber' */ });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `to` | string | yes | Destination id (agent, queue or PSTN number). |
| `destinationType` | string | yes | One of `agent`, `queue` or `dialNumber`. |

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

## Consult and Consult Transfer (Telephony)

### Start Consult

Start a consult with an agent, queue or a PSTN number

```javascript
await currentTask.consult({ to: '<DEST_ID>', destinationType: 'agent' /* or 'queue' or 'dialNumber' */ });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `to` | string | yes | Destination id (agent, queue or PSTN number). |
| `destinationType` | string | yes | One of `agent`, `queue` or `dialNumber`. |
| `holdParticipants` | boolean | no | Whether to hold other participants (defaults to true). |

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

#### Relevant Task Events

- `task:consultCreated` — When a consult is initiated.
- `task:offerConsult` — When a consult offe is received.
- `task:consulting` — When the consult is in progress.
- `task:consultAccepted` — When an incoming consult is accepted.
- `task:consultQueueFailed` — When consult to queue fails.

### End Consult

End the current consult leg or cancel a queued consult.

```javascript
await currentTask.endConsult({ isConsult: true, taskId: currentTask.data?.interactionId /*, queueId */ });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `isConsult` | boolean | yes | Must be true to indicate consult termination. |
| `taskId` | string | yes | Task interaction id. |
| `queueId` | string | conditional | Required when ending a queue consult before it is accepted. |

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

#### Relevant Task Events

- `task:consultEnd`
- `task:consultQueueCancelled` (when queue consult is cancelled)

### Consult Transfer

Transfer the main call to the consulted agent and leave the call.

```javascript
await currentTask.consultTransfer({ to: '<DEST_ID>', destinationType: 'agent' /* or 'queue' or 'dialNumber' */ });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `to` | string | yes | Destination id (agent, queue or PSTN number). |
| `destinationType` | string | yes | One of `agent`, `queue` or `dialNumber`. |

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

## End and Wrap-up

### End Task

End the active task.

```javascript
await currentTask.end();
```

#### Request Parameters
No parameters.

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse).

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

## Outbound Dialing (Telephony)

Initiate an outbound telephony call from the agent.

```javascript
await webex.cc.startOutdial('<E164_OR_VALID_NUMBER>'); // E164 is an International Standard of Telephone numbers
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `destination` | string | yes | Phone number to dial (prefer E.164). |

#### Response Payload

- Resolves with a [TaskResponse](#taskresponse) (includes identifiers like `interactionId`).

Ensure the agent is allowed to outdial and in the correct state.

## Destination Lists for Transfer/Consult

Populate destinations using the plugin APIs:

```javascript
const queues = await webex.cc.getQueues(); // filter by channelType === 'TELEPHONY' if needed
const buddies = await webex.cc.getBuddyAgents({ mediaType: 'telephony' });
```

#### Queue Item (example fields)

| key | description |
| --- | --- |
| `id` | Queue id used for consult/transfer. |
| `name` | Queue display name. |
| `channelType` | Channel type (e.g., `TELEPHONY`). |

#### Buddy Agent Item (example fields)

| key | description |
| --- | --- |
| `agentId` | Agent id to consult/transfer. |
| `agentName` | Display name shown in UI. |
| `state` | Agent state (e.g., Available/Idle). |

## Task Events (Common)

These events are commonly used when building task UIs:
- `task:incoming`: New inbound task is offered to the agent.
- `task:hydrate`: When UI reloads (ie. relogin case) and an existing task was present. The payload is delivered to refresh local UI/state.
- `task:assigned`: Task was successfully accepted and assigned to the agent.
- `task:media` (telephony): Remote audio track is available; attach it to an `<audio>` element.
- `REAL_TIME_TRANSCRIPTION`: A real-time transcript payload was received for the interaction.
- `task:hold` (telephony): Active telephony leg was placed on hold.
- `task:resume` (telephony): Active telephony leg was resumed from hold.
- `task:consultCreated` (telephony): A consult leg was initiated by the agent.
- `task:offerConsult` (telephony): An incoming consult offer was received.
- `task:consultAccepted` (telephony): The consult offer was accepted and connected.
- `task:consulting` (telephony): Consult is in progress (connected state).
- `task:consultQueueFailed` (telephony): Consult to a queue failed to connect.
- `task:consultQueueCancelled` (telephony): Queue consult was cancelled before connection.
- `task:consultEnd` (telephony): Consult leg ended.
- `task:end`: Task ended; includes wrap-up info like `wrapUpRequired`.
- `task:wrappedup`: Wrap‑up completed and submitted.
- `task:rejected`: Task was rejected or went unanswered; includes reason also (ie. rejected or unavailable).

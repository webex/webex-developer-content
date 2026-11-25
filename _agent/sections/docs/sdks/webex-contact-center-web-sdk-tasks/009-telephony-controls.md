---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Telephony Controls
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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

#### Relevant Task Events

- `task:recordingResumed`
- `task:recordingResumeFailed`

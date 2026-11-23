---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Consult and Consult Transfer (Telephony)
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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

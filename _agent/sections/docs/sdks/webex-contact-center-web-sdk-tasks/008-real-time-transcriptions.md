---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Real-time Transcriptions
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

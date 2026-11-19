---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Transfer (All Channels Where Supported)
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

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse).

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Accept Task
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

## Accept Task

Accept an offered task.

```javascript
await currentTask.accept();
```

#### Request Parameters
No parameters.

#### Response Payload

- Telephony (BROWSER): resolves with no payload.
- Digital (chat, email, social): resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse) object (includes at least `trackingId`).

#### Relevant Task Events

- `task:assigned` — Emitted when the task has been successfully accepted.
- `task:media` — Emitted for telephony tasks with a remote audio track.

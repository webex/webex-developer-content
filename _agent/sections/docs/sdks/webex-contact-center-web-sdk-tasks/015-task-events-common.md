---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Task Events (Common)
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

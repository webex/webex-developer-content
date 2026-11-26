---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Response Type: TaskResponse'
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

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Selecting and Handling a Task
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

## Selecting and Handling a Task

When a task is selected, update the UI and enable/disable controls based on the channel and state. For example, telephony tasks expose voice controls, while digital tasks do not.

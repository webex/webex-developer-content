---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- API and event reference
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md) [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## API and event reference

### Configuration and task methods

| Configuration or method | Purpose |
| --- | --- |
| `config.cc.enableWxBetterTogether` | Enable the flow before SDK initialization and station login. |
| `task.accept()` | Accept an offered Webex App voice task. |
| `task.decline()` | Decline an inbound offer or cancel an outbound ringing offer. |
| `task.toggleMute({ muted })` | Set the intended Webex App mute state on an engaged call. |
| `task.getWxAppMuted()` | Read the SDK-cached mute state. |
| `task.syncWxAppMuteFromCallDetails()` | Asynchronously refresh mute state from call details. |
| `task.transmitDtmf({ dtmf })` | Send in-call keypad digits. |

### Events

| Subscribe on | Event | Host action |
| --- | --- | --- |
| `webex.cc` | `task:incoming` | Add the offered task to the UI and attach its control listener. |
| `webex.cc` | `task:hydrate` | Restore task bindings after reload or reconnect. |
| `task` | `task:ui-controls-updated` | Refresh control visibility and enabled state. |
| `task` | `task:assigned` | Attach mute synchronization and seed mute state when the task becomes the active engaged call. |
| `task` | `task:rejected` | Clear an offer that is rejected or goes unanswered. |
| `task` | `task:wxapp-mute-state-updated` | Update the mute icon from the `{ muted }` payload. |
| `task` | `task:end` | Detach listeners when the task ends. |

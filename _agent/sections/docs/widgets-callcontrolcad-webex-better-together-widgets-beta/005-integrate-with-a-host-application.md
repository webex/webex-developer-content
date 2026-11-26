---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Integrate with a host application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [Release scope and limitations](006-release-scope-and-limitations.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Integrate with a host application

The feature uses existing widget exports. Enable the feature before initialization, then render the normal IncomingTask, TaskList, and CallControl widgets in the host’s layout. The SDK updates control visibility and enabled state according to the task and login type.

- **Incoming offers:** Accept and Decline are available for supported wxApp voice offers. `IncomingTask` resolves the live task from `store.taskList` by `interactionId`, so the Accept control stays current when SDK controls update. Pass the store-provided `incomingTask` prop.
- **Offer errors:** If accept or decline fails, the offer card shows an inline error. The shared `offerActionErrors` map is keyed by `interactionId`, keeping `TaskList` and `IncomingTask` consistent for the same interaction.
- **Mute:** `CallControl` exposes Mute for an engaged wxApp call when the flag is enabled. The widget passes explicit intent to `task.toggleMute({ muted })`; mute changes made in Webex App update the embedded control through the SDK event `task:wxapp-mute-state-updated` and the store’s `isMuted` state.
- **Keypad:** `CallControl` exposes Keypad under the same engaged-call condition. It sends digits with `task.transmitDtmf({ dtmf })`. The widget keypad accepts `0`–`9`, `*`, and `#`; commas and other characters are discarded.
- **Other call actions:** Hold, resume, transfer, consult, conference, end, wrap-up, and recording continue to use their existing SDK and widget paths.

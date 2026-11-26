---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Release scope and limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Release scope and limitations

This beta supports Accept and Decline on Webex App voice offers, bidirectional Mute synchronization, in-call DTMF, toast suppression when enabled, and Extension or Agent DN station login.

The following are not supported in this release:

- Hold-state synchronization with Webex App. Existing hold and resume actions may not match the Webex App state.
- Browser/WebRTC station login as the Webex Better Together answer path.
- Webex App on mobile or tablet as the primary answer client.
- Full removal of the Webex mini call window.
- Changing `enableWxBetterTogether` after initialization.

Only one client should answer a given offer. `allowMultiLogin: true` is supported, but `allowMultiLogin: false` is recommended for a single CRM embed session per agent.

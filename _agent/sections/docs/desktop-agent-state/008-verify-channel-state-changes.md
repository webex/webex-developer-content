---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-agent-state
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify Channel State Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-agent-state). [Full Markdown](../../../../docs/desktop-agent-state.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Read agent information and manage availability by media channel with the Desktop SDK.

## Selected section

## Verify Channel State Changes

When using `stateChangeV2`, listen for `eAgentChannelStateChanged` and read the corresponding entry in `STORE.agent.channelsStatesMap`. The `updated` event does not report the granular state changes. See [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout).

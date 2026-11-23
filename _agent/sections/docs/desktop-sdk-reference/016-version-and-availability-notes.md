---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-reference
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Version and Availability Notes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-reference). [Full Markdown](../../../../docs/desktop-sdk-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Desktop SDK modules, methods, properties, and events with links to their detailed reference pages.

## Selected section

## Version and Availability Notes

- The SDK runs in widgets embedded within Desktop; it does not create a separate Desktop.
- With granular state control, use `stateChangeV2`, `STORE.agent.channelsStatesMap`, and `eAgentChannelStateChanged`. Global `subStatus` and the `updated` state-change event are not valid for that flow.
- The Popover APIs are available only in the isolated environment Desktop provides for custom widgets.
- The Webex Metrics module is documented as internal; its presence in this index does not establish availability for third-party widgets.

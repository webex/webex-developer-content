---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- acceptWebRtcCall()
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-call-control). [Full Markdown](../../../../docs/desktop-call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Retrieve tasks and control interactions, WebRTC calls, and call recording from Desktop widgets.

## Parent context

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

## Selected section

### acceptWebRtcCall()

Accepts an incoming WebRTC call. This method allows agents to answer WebRTC-based voice calls routed through the contact center.

**Example**

```javascript
await Desktop.actions.acceptWebRtcCall();
// => Accept the incoming WebRTC call
```

Returns
 The response will be similar to the "AgentContactAssigned" event.

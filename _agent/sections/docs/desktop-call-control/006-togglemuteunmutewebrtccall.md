---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Desktop Actions
- toggleMuteUnmuteWebRtcCall()
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

### toggleMuteUnmuteWebRtcCall()

Toggles the mute/unmute state for an active WebRTC call. This method switches between muted and unmuted states for the agent's microphone during an ongoing WebRTC call session.

**Example**

```javascript
await Desktop.actions.toggleMuteUnmuteWebRtcCall();
// => Toggle mute/unmute state for the current WebRTC call
```

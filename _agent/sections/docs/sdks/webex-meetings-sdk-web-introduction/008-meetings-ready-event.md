---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings Ready Event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

## Meetings Ready Event

A `meetings:ready` event fires when a `meetings` object is ready for use. A `meetings` object instance is ready once the containing `Webex` object is ready, and all the `meetings` object's instance parameters are set. You can subscribe to the ready event immediately following `Webex.init`:

```js
webex.meetings.on('meetings:ready',() => {
  console.log('Meetings object is ready for device registration');
  // Register a new device...
});
```

The ready event returns no payload. 



> **Info**
>
> Make any Meetings object method calls only after receiving this event.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Network Disconnected Event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

## Network Disconnected Event

The `network:disconnected` event fires when a meeting instance is disconnected from the Webex Cloud server or when the browser's local network is disconnected:

```js
webex.meetings.on('network:disconnected', () => {
  // Perform operations to cleanup the UI that is related to a Meeting Leave
});
```

### Network Connected Event

The `network:connected` event fires when the meetings instance is reconnected to the network after being disconnected:

```js
webex.meetings.on('network:connected', () => {
  //Perform operations to reconnect Meeting
});
```

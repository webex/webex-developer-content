---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Enable Multistream
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-multistream-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Setup Remote Media Event Listeners](004-setup-remote-media-event-listeners.md)

## Article introduction

With multistream, developers gain greater flexibility when displaying remote media streams. Instead of receiving a single stream featuring all participants, multistream enables the showcasing of multiple streams simultaneously. This means you can easily view each remote participant's stream individually, enhancing clarity and engagement during collaborative sessions.

---

This guide provides a quick glimpse into consuming multistream in Webex Meetings using the Webex JavaScript SDK. You'll find code snippets below that can quickly get you up and running.

## Selected section

## Enable Multistream

To integrate multistream functionality into your meetings, include the `enableMultistream` flag within the `joinOptions` parameter when calling either the `meeting.join()` or `meeting.joinWithMedia()` methods:

```js
const joinOptions = {
  enableMultistream: true,
  ...
};

// Use either the join() method:

await meeting.join(joinOptions);

// ...or the joinWithMedia() method:

await meeting.joinWithMedia({joinOptions, mediaOptions});
```



> **Info**
>
> For additional details, see [Join a Meeting](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting).

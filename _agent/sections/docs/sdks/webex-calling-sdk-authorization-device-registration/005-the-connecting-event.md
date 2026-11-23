---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- The Connecting Event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Selected section

## The Connecting Event

By listening for the `connecting` event,  the app can determine that it's in the connecting state once the `register()` call is made: 

```js
line.on('connecting', () => {
    // Store the line registration details
}
```

This event has no payload. If the event listener is triggered, it means the line is connecting.

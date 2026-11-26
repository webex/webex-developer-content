---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings Ready Event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device registration are important first steps in starting a meeting using the Web SDK. This document helps in using SDK for authenticating a user and registering the device with the Webex Meetings servers.

## Selected section

## Meetings Ready Event

A `ready` event fires when a `Meetings` object is ready for use. A `Meetings` object instance is ready once the containing `Webex` object is ready, and all the `Meetings` object's instance parameters are set. You can subscribe to the ready event immediately following `Webex.init`:

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

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Retrieve a Meeting Object
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device registration are important first steps in starting a meeting using the Web SDK. This document helps in using SDK for authenticating a user and registering the device with the Webex Meetings servers.

## Selected section

## Retrieve a Meeting Object

The `Meetings` object is accessible from the `Webex` object:

```js
const webex = new Webex.init();
const meetings = webex.meetings;
```

The `meetings` constant contains an instance of the Webex `Meetings` object.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Initialize the SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device registration are important first steps in starting a meeting using the Web SDK. This document helps in using SDK for authenticating a user and registering the device with the Webex Meetings servers.

## Selected section

## Initialize the SDK

To use the SDK, you'll need a free Webex account; if you don't have a Cisco Webex account, visit [Cisco Webex for Developers](https://developer.webex.com/) to create your account and retrieve your **access token** from [Getting and Using your Personal Access Token](https://developer.webex.com/docs/getting-your-personal-access-token).

To create a new Webex instance:

```js
const webex = Webex.init({
    credentials: {  
       access_token: `<AUTHORIZATION/BOT TOKEN>`
    }
});
```

At this point, the Webex `Meetings` object is ready for use. The `Meetings` object contains a list of meetings as well as methods to perform specific operations or listen for certain events. Detailed information is included in this article.

For more information on the `Meetings` object, see the [Webex Meetings Quickstart](https://developer.webex.com/meeting/docs/sdks/webex-meetings-sdk-web-quickstart).

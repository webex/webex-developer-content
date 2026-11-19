---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Enable Webex Better Together before initialization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md) [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## Enable Webex Better Together before initialization

Use an access token for the same user who is signed in to Webex App: an OAuth user token for an integration or a Personal Access Token (PAT) for testing. For OAuth integrations, request `spark:calls_write` for call controls and `spark:calls_read` for mute-state read-back, in addition to the Contact Center scopes. Reauthorize the user after adding these scopes to an existing integration. Bot tokens are not supported for this flow.

Import the SDK and set the flag in the options passed to `Webex.init()`. Obtain `token` through the [Authentication guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication).

```js
import Webex from '@webex/contact-center';

const webex = Webex.init({
  credentials: {
    access_token: token,
  },
  config: {
    cc: {
      enableWxBetterTogether: true,
      allowMultiLogin: false,
    },
  },
});

// Capture readiness immediately after initialization.
const sdkReady = new Promise((resolve) => webex.once('ready', resolve));
```

Wait for the SDK's `ready` event before registering, then complete station login with your assigned team and Extension or Agent DN. Replace the example values below with your agent's configuration.

```js
await sdkReady;
await webex.cc.register();
await webex.cc.stationLogin({
  teamId: '<TEAM_ID>',
  loginOption: 'EXTENSION', // Use 'AGENT_DN' for an Agent DN login.
  dialNumber: '<EXTENSION_OR_DN>',
});
```

Only one client should answer a given offer. `allowMultiLogin: true` is supported, but `allowMultiLogin: false` is recommended for a single CRM embed session per agent. See the [Quickstart guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication guide](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication) for the full initialization, login, and agent-state flow.

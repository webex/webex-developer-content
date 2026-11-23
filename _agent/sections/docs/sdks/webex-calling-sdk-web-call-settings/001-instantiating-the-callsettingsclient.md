---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Instantiating the CallSettingsClient
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-call-settings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article explains the various call settings that are available in the Calling SDK. 

---

The Calling SDK consists of various modules which are created at the time of its initialization--`CallSettingsClient` is one of those modules. Refer to the [Getting Started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how a calling instance is created and different modules are instantiated.

The `CallSettingsClient` lets you fetch and update user-specific settings for the following features:

- Do not disturb (DND)
- Call Forwarding
- Voicemail
- Call Waiting

## Selected section

## Instantiating the CallSettingsClient

The `CallSettingsClient` is implemented as the `CallSettings` class in the SDK and there are two ways of instantiating it.

To instantiate just the `CallSettingsClient`, use the `createCallSettingsClient` method:

```javascript
const callSettings = createCallSettingsClient(webex, logger);
```

If the `CallSettingsClient` is initialized through the `calling` instantiation:

```javascript
const callSettings = calling.callSettingsClient;
```

Developers have the option to select from multiple backends when working with the Calling SDK, including UCM, Broadworks, and WXCalling. Those backends share similar APIs and implementation methodologies, ensuring a consistent development experience. However, it's important to be aware that certain APIs are specific to particular backends, such as `getCallForwardAlways`, which is exclusive to the UCM backend.

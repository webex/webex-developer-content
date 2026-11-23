---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- CallSettingResponse Object
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

## CallSettingResponse Object

All methods within `callSettingsClient` return a standardized response type known as the `CallSettingResponse`. This response type encompasses three key components: the status code, data, and message. The `data` component of this response object serves as a container for either the `callSettings` object or the `error` object, depending on whether the API call was successful or encountered an issue.

The `callSettings` object, present in the `data` field, contains a variety of data types, each specific to the API invoked. These data types are as follows:

- ToggleSetting
- CallForwardSetting
- VoicemailSetting
- CallForwardAlwaysSetting

### CallSettingResponse Example

```js
{
  statusCode: number;
  data: {
    callSetting?: ToggleSetting | CallForwardSetting | VoicemailSetting | CallForwardAlwaysSetting;
    error?: string;
  };
  message: string | null;
};
```

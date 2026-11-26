---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Waiting
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

## Call Waiting

### Get Call Waiting Settings Method

Call waiting allows users to receive incoming calls while they are already on an active call. When call waiting is enabled, the user is notified of an incoming call and given the option to put the current call on hold temporarily to answer the new call. The `getCallWaitingSetting()` method retrieves the call waiting settings for a user.

```js
const response = await callSettings.getCallWaitingSetting();
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | --                                                   |
| **Returns**    | `Promise<CallSettingResponse>` |

Here's an example of a response for a successful `getCallWaitingSetting()` method call:

```js
{
    "statusCode": 200,
    "data": {
        "callSetting": {
            "enabled": true
        }
    },
    "message": "SUCCESS"
}
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Do Not Disturb (DND)
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

## Do Not Disturb (DND)

The DND feature allows users to temporarily disable notifications or incoming communication on their devices. This feature comprises two available methods: `getDoNotDisturbSetting()` and `setDoNotDisturbSetting()`.

### Fetch DND Status Method

This method retrieves the Do Not Disturb (DND) setting for a user. By default, DND is disabled for users. However, should a user choose to modify their DND setting, this method returns the updated value. The method returns a `ToggleSetting` object in the `callSetting` object of the response.

```js
const response = await callSettings.getDoNotDisturbSetting();
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | --                                                   |
| **Returns**    | Promise<[CallSettingResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings#callSettingResponse)> |

### ToggleSetting Object

When the API response is successful, it includes a specific data structure called `ToggleSetting` within the `callSettings` object. The `ToggleSetting` object contains various attributes that provide information related to the Do Not Disturb (DND) setting.

The following table covers the attributes present in the `ToggleSetting` object:



| **Name** | **Description** | **Type** | **Required** |
| --- | --- | --- | --- |
| `enabled` | `true` if the Do Not Disturb feature is enabled. | `Boolean` | Yes |
| `ringSplashEnabled` | Enables a Ring Reminder to play a brief tone on a desktop phone when an incoming call is received. | `Boolean` | Yes |

Here's an example of a response for a successful `getDoNotDisturbSetting()` retrieval of the DND settings:

```js
{
    "statusCode": 200,
    "data": {
        "callSetting": {
            "enabled": false,
            "ringSplashEnabled": false
        }
    },
    "message": "SUCCESS"
}
```

### Set DND Status Method

The `setDoNotDisturbSetting()` method configures the Do Not Disturb (DND) status for a user. Using this method, you can let users adjust their DND status as needed. The method accepts a `boolean` parameter which, when to `true`, activates DND, and when set to `false`, deactivates DND.

```java
const response = await callSettings.setDoNotDisturbSetting(true);
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | `Boolean`                                              |
| **Returns**    | Promise<[CallSettingResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings#callSettingResponse)> |

If method call is successful, it returns a new `ToggleSetting` object in the `callSetting` object of the response. 

Here's an example of the response for the `setDoNotDisturbSetting(flag)` method:

```js
{
    "statusCode": 204,
    "data": {
        "callSetting": {
            "enabled": false,
            "ringSplashEnabled": false
        }
    },
    "message": "SUCCESS"
}
```

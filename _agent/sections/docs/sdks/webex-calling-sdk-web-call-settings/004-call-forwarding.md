---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Forwarding
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

## Call Forwarding

The Call Forwarding feature allows you to redirect incoming calls to a different phone number or extension, ensuring users never miss important calls. This feature comprises two methods `getCallForwardSetting()` and `setCallForwardSetting()`.

### Get Call Forwarding Settings Method

The `getCallForwardSetting()` method facilitates the retrieval of call-forwarding settings for a user. Within the Calling SDK, developers have the flexibility to configure call forwarding preferences, including settings for scenarios such as when the user is engaged in another call, when an incoming call remains unanswered, and even when the user wishes to forward all incoming calls.

Upon a successful method call, the response includes the `CallForwardSetting` in the `callSetting` object.

```js
const response = await callSettings.getCallForwardSetting();
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | --                                                   |
| **Returns**    | Promise<[CallSettingResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings#callSettingResponse)> |

Here's an example of the response for a successful `getCallForwardSetting()` method call:

```js
{
  "statusCode": 200,
  "data": {
    "callSetting": {
      "callForwarding": {
        "always": {
          "enabled": false,
          "ringReminderEnabled": false,
          "destinationVoicemailEnabled": false
        },
        "busy": {
          "enabled": false,
          "destinationVoicemailEnabled": false
        },
        "noAnswer": {
          "enabled": false,
          "numberOfRings": 3,
          "systemMaxNumberOfRings": 20,
          "destinationVoicemailEnabled": false
        }
      },
      "businessContinuity": {
        "enabled": false,
        "destinationVoicemailEnabled": false
      }
    }
  },
  "message": "SUCCESS"
}

```

### Get Call Forward Always Settings Method

The `getCallForwardAlwaysSetting()` method allows users to ensure that all incoming calls, regardless of their current status or availability, are automatically redirected to a designated destination. This API is designed for fetching the call forwarding always setting, with an added functionality to verify the call forwarding always setting for voicemail. In cases where call forwarding is configured to a specific destination, that destination takes precedence.

The method accepts a directory number for which you wish to retrieve the settings. On success, the response includes the `CallForwardAlwaysSetting` in the `callSetting` object.

```js
const directoryNumber = '123456789';
const response = await callSettings.getCallForwardAlwaysSetting(directoryNumber);
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | `string`                                               |
| **Returns**    | Promise<[CallSettingResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings#callSettingResponse)> |

### CallForwardAlwaysSetting Object

The `getCallForwardAlwaysSetting()` method returns a `CallForwardAlwaysSetting` object in a `callSetting` object. The following table describes the attributes in the `CallForwardAlwaysSetting` object, followed by an example code block:



| **S.no** | **Name** | **Description** | **Type** | **Required** |
| --- | --- | --- | --- | --- |
| 1. | `enabled` | 'Always' call forwarding is enabled/disabled. | `Object` | Yes |
| 2. | `ringReminderEnabled` | If `true`, a brief tone will be played on the person's phone when a call has been forwarded. | `Boolean` | No |
| 3. | `destinationVoicemailEnabled` | Indicates the enabled or disabled state of sending incoming calls to voicemail when the destination is an internal phone number and that number has the voicemail service enabled. | `Boolean` | No |
| 4. | `destination` | Destination for 'always' call forwarding | `String` | No |

```js
{
  statusCode: 204,
  data: {
    callSetting: {
      callForwarding: {
        enabled: false,
        destination: '',
        ringReminderEnabled: false,
        destinationVoicemailEnabled: false,
      },
    },
  },
  message: 'SUCCESS',
};
```

### Set Call Forwarding Settings Method

This API configures call-forwarding settings for a specific user. Upon successful execution, it provides a `CallForwardSetting` object within the `callSetting` object. The `CallForwardSetting` object comprises individual objects for three scenarios, "Always", "Busy", and "No Answer". Developers can use this object to indicate their preferences for call forwarding in those specific situations. Additionally, the API supports business continuity by enabling users to forward calls even when they are not currently connected to any network.

```js
const response = await callSettings.setCallForwardSetting(callForwardingSettings);
```


|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | [CallForwardSetting](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings#callForwardSetting)            |
| **Returns**    | Promise<[CallSettingResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings#callSettingResponse)> |

### CallForwardSetting Object

The `setCallForwarding()` method accepts a `CallForwardSetting` object. The following table covers the attributes in the `CallForwardSetting` object:



| **S.no** | **Name** | **Description** | **Type** | **Required** |
| --- | --- | --- | --- | --- |
| 1. | `callForwarding` | Settings related to "Always", "Busy", and "No Answer" call forwarding. | `Object` | Yes |
| 1.1 | `always` | Settings for forwarding all incoming calls. | `Object` | Yes |
| 1.1.a | `enabled` | "Always" call forwarding is enabled/disabled. | `Boolean` | Yes |
| 1.1.b | `destination` | Destination for "Always" call forwarding. | `String` | No |
| 1.1.c | `ringReminderEnabled` | If `true`, a brief tone will be played on the person's phone when a call has been forwarded. | `Boolean` | No |
| 1.1.d | `destinationVoicemailEnabled` | Indicates the enabled or disabled state of sending incoming calls to voicemail when the destination is an internal phone number and that number has the voicemail service enabled. | `Boolean` | No |
| 1.2 | `busy` | Setting for forwarding incoming calls when a person is busy. | `Object` | Yes |
| 1.2.a | `enabled` | "Busy" call forwarding enabled/disabled. | `Boolean` | Yes |
| 1.2.b | `destination` | Destination for "Busy" call forwarding. | `String` | No |
| 1.2.c | `destinationVoicemailEnabled` | Indicates the enabled or disabled state of sending incoming calls to voicemail when the destination is an internal phone number and that number has the voicemail service enabled. | `Boolean` | No |
| 1.3 | `noAnswer` | Settings for forwarding when the call is not answered. | `Object` | Yes |
| 1.3.a | `enabled` | "No Answer" call forwarding enabled/disabled. | `Boolean` | Yes |
| 1.3.b | `destination` | Destination for "No Answer" call forwarding. | `String` | No |
| 1.3.c | `numberOfRings` | The number of rings before the call will be forwarded if unanswered. | `Number` | No |
| 1.3.d | `systemMaxNumberOfRings` | System-wide maximum number of rings allowed for `numberOfRings` setting. | `Number` | No |
| 1.3.e | `destinationVoicemailEnabled` | Indicates the enabled or disabled state of sending incoming calls to voicemail when the destination is an internal phone number and that number has the voicemail service enabled. | `Boolean` | No |
| 2. | `businessContinuity` | Settings for sending calls to a destination of your choice if your phone is not connected to the network. | `Object` | Yes |
| 2.1 | `enabled` | Business Continuity is enabled or disabled. | `Boolean` | Yes |
| 2.2 | `destination` | Destination for Business Continuity. | `String` | No |
| 2.3 | `destinationVoicemailEnabled` | Indicates the enabled or disabled state of sending incoming calls to the destination number's voicemail if the destination is an internal phone number and that number has the voicemail service enabled. | `Boolean` | No |

Here's an example of a `CallForwardSetting` object:

```js
const callForwardingSettings = {
  callForwarding: {
    always: {
      enabled: false
    },
    busy: {
      enabled: false
    },
    noAnswer: {
      enabled: true,
      destination: '123123',
      numberOfRings: 3
    }
  },
  businessContinuity: {
    enabled: true,
    destination: '321321',
    destinationVoicemailEnabled: false
  }
};
```

Here's an example of a response for the `setCallForwardingSetting()` method:

```js
{
  "statusCode": 204,
  "data": {
    "callSetting": {
      "callForwarding": {
        "always": {
          "enabled": false,
          "destination": "",
          "ringReminderEnabled": false,
          "destinationVoicemailEnabled": false
        },
        "busy": {
          "enabled": true,
          "destination": "9075551333",
          "destinationVoicemailEnabled": true
        },
        "noAnswer": {
          "enabled": false,
          "destination": "",
          "numberOfRings": 2,
          "systemMaxNumberOfRings": 20,
          "destinationVoicemailEnabled": false
        }
      },
      "businessContinuity": {
        "enabled": false,
        "destination": "",
        "destinationVoicemailEnabled": false
      }
    }
  },
  "message": "SUCCESS"
}

```

---
type: Guide
title: Web Calling SDK | Call Settings
display_title: Call Settings
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings)

This article explains the various call settings that are available in the Calling SDK. 

---

The Calling SDK consists of various modules which are created at the time of its initialization--`CallSettingsClient` is one of those modules. Refer to the [Getting Started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how a calling instance is created and different modules are instantiated.

The `CallSettingsClient` lets you fetch and update user-specific settings for the following features:

- Do not disturb (DND)
- Call Forwarding
- Voicemail
- Call Waiting

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
| **Returns**    | Promise<[CallSettingResponse](#callSettingResponse)> |

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
| **Returns**    | Promise<[CallSettingResponse](#callSettingResponse)> |

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
| **Returns**    | Promise<[CallSettingResponse](#callSettingResponse)> |

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
| **Returns**    | Promise<[CallSettingResponse](#callSettingResponse)> |

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
| **Parameters** | [CallForwardSetting](#callForwardSetting)            |
| **Returns**    | Promise<[CallSettingResponse](#callSettingResponse)> |

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

## Voicemail

### Fetch Voicemail Settings Method

The `getVoicemailSetting()` method is used to retrieve the voicemail configuration settings for a user. If the method call is successful, it returns a `VoicemailSetting` object within a `callSetting` object.

```js
const response = await callSettings.getVoicemailSetting();
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | --                                                   |
| **Returns**    | Promise<`CallSettingResponse`> |

Here's an example of a response for a successful `getVoicemailSetting()` method call:

```js
{
    "statusCode": 200,
    "data": {
        "callSetting": {
            "enabled": true,
            "sendAllCalls": {
                "enabled": false
            },
            "sendBusyCalls": {
                "enabled": true,
                "greeting": "DEFAULT",
                "greetingUploaded": false
            },
            "sendUnansweredCalls": {
                "enabled": true,
                "greeting": "DEFAULT",
                "greetingUploaded": false,
                "numberOfRings": 3,
                "systemMaxNumberOfRings": 20
            },
            "notifications": {
                "enabled": false
            },
            "transferToNumber": {
                "enabled": false
            },
            "emailCopyOfMessage": {
                "enabled": false
            },
            "messageStorage": {
                "mwiEnabled": true,
                "storageType": "INTERNAL",
                "externalEmail": "atlas.test.wxcwebrtc.user50+client5@example.com"
            },
            "faxMessage": {
                "enabled": false
            },
            "voiceMessageForwardingEnabled": true
        }
    },
    "message": "SUCCESS"
}
```

### Set Voicemail Settings Method

The `setVoicemailSetting()` method lets you make choices regarding call handling: you can route callers to voicemail when a user is occupied, when a call goes unanswered, or choose to direct all incoming calls to voicemail. If the method call is successful it returns a `VoicemailSetting` object in the `callSetting` object.

```js
const response = await callSettings.setVoicemailSetting(voicemailSetting);
```



|                |                                                      |
| -------------- | ---------------------------------------------------- |
| **Parameters** | `VoicemailSetting`               |
| **Returns**    | `Promise<CallSettingResponse>` |

### VoicemailSetting Object

`setVoicemailSetting()` accepts a `VoicemailSetting` object. The following table covers the attributes in the `VoicemailSetting` object:



| **S.no** | **Name** | **Description** | **Type** | **Required** |
| --- | --- | --- | --- | --- |
| 1. | `enabled` | Voicemail is enabled or disabled. | `Boolean` | Yes |
| 2. | `sendAllCalls` | Settings for sending all calls to voicemail. | `Object` | Yes |
| 2. a | `enabled` | All calls will be sent to voicemail. | `Boolean` | Yes |
| 3. | `sendBusyCalls` | Settings for sending calls to voicemail when the line is busy. | `Object` | Yes |
| 3. a | `enabled` | Calls will be sent to voicemail when busy. | `Boolean` | Yes |
| 3. b | `greeting` | Type of greeting to be played, 'default' or 'custom'. | `String` | No |
| 3. c | `greetingUploaded` | True if a custom greeting is uploaded. | `Boolean` | No |
| 4. | `sendUnansweredCalls` | Settings for sending calls to voicemail when the line is busy. | `Object` | Yes |
| 4. a | `enabled` | Unanswered call sent to voicemail is enabled or disabled. | `Boolean` | Yes |
| 4. b | `greeting` | Type of greeting to be played, 'default' or 'custom'. | `String` | No |
| 4. c | `greetingUploaded` | True if a custom greeting is uploaded. | `Boolean` | No |
| 4. d | `numberOfRings` | The number of rings before an unanswered call will be sent to voicemail. | `Number` | Yes |
| 4. e | `systemMaxNumberOfRings` | System-wide maximum number of rings allowed for the `numberOfRings` setting. | `Number` | No |
| 5. | `notifications` | Settings for notifications when there are any new voicemails. | `Object` | Yes |
| 5. a | `enabled` | Notifications for voicemails will be sent. | `Boolean` | Yes |
| 5. b | `destination` | Email address to which the notification will be sent. | `String` | No |
| 6. | `transferToNumber` | Settings for voicemail caller to transfer to a different number by pressing zero (0). | `Object` | No |
| 6. a | `enabled` | Enable or disable voicemail caller transfer to a destination by pressing zero (0). | `Boolean` | No |
| 6. b | `destination` | The number voicemail caller will be transferred to when they press zero (0). | `String` | No |
| 7. | `emailCopyOfMessage` | Settings for sending a copy of new voicemail message audio via email. | `Object` | Yes |
| 7. a | `enabled` | When `true` copy of the new voicemail message audio will be sent to the designated email. | `Boolean` | Yes |
| 7. b | `emailId` | Email address to which the new voicemail audio will be sent. | `String` | No |
| 8. | `messageStorage` | Settings for storage for new voicemails. | `Object` | Yes |
| 8. a | `mwiEnabled` | When `true` desktop phone will indicate there are new voicemails. | `Boolean` | Yes |
| 8. b | `storageType` | Designates which type of voicemail message storage is used, 'internal' or 'external'. | `String` | Yes |
| 8. c | `externalEmail` | External email address to which the new voicemail audio will be sent. | `String` | No |
| 9. | `faxMessage` | Settings for FAX messages for new voicemails. | `Object` | No |
| 9. a | `enabled` | When `true` FAX messages for new voicemails will be sent to the designated number. | `Boolean` | No |
| 9. b | `phoneNumber` | Designates phone number for FAX. | `String` | No |
| 9. c | `extension` | Designates optional extension for FAX. | `String` | No |
| 10. | `voiceMessageForwardingEnabled` | If `true` voicemail forwarding is enabled. | `Boolean` | No |

Here's an example of a configured `VoiceMailSetting` object along with a call to the `setVoicemailSetting()` method:

```js
const voicemailSetting = {
  enabled: true,
  sendAllCalls: {
    enabled: false
  },
  sendBusyCalls: {
    enabled: true
  },
  sendUnansweredCalls: {
    enabled: true,
    numberOfRings: 3
  },
  notifications: {
    enabled: true,
    destination: dummyEmail
  },
  emailCopyOfMessage: {
    enabled: true,
    emailId: dummyEmail
  },
  messageStorage: {
    mwiEnabled: true,
    storageType: 'INTERNAL',
    externalEmail: dummyEmail
  },
  voiceMessageForwardingEnabled: false
};

const response = await callSettingsClient.setVoicemailSetting(voicemailSetting);
```

Here's an example of a response for a successful `setVoicemailSetting()` call:

```js
{
    "statusCode": 204,
    "data": {
        "callSetting": {
            "enabled": true,
            "sendAllCalls": {
                "enabled": false
            },
            "sendBusyCalls": {
                "enabled": true
            },
            "sendUnansweredCalls": {
                "enabled": false
            },
            "notifications": {
                "enabled": false
            },
            "emailCopyOfMessage": {
                "enabled": false
            },
            "messageStorage": {
                "mwiEnabled": true
            }
        }
    },
    "message": "SUCCESS"
}
```

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

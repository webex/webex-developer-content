---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-settings
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Voicemail
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

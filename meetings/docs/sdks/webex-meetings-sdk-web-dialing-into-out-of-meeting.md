---
type: Guide
title: Web Meetings SDK | Dialing Into or Out of a Meeting
display_title: Dialing In and Out
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting)

When connected to a meeting, the following dialing capabilities are available:

- **Dial out**: Allows the system to call a user's phone, enabling it to be used as the audio input/output device for the meeting.
- **Dial in**: Permits users to call into Webex and use their phone as the meeting's audio input/output device.

<br/>

The SDK also provides functionality to remotely end phone calls in both of the above scenarios.

## Dial Into or Out of a Meeting

A user can trigger the dial-in or dial-out using the `Meeting` object's [usePhoneAudio](https://webex.github.io/webex-js-sdk/api/#meetingusephoneaudio) method and passing an optional phone number as a String:

```js
await meeting.usePhoneAudio(phoneNumber);
```



|  |  |
| --- | --- |
| **Asynchronous** | Yes |
| **Parameters** | **String** - `phoneNumber` (Optional) |
| **Returns** | `Promise` Resolves once the dial-in or dial-out request gets completed, or rejects if it fails |

When a phone number is provided, the SDK provisions a device for dial out functionality, and initiates a call to the specified phone number. When a user answers the call, the meeting's audio input and output are connected to the phone device. In the absence of a phone number, the SDK defaults to provisioning a device for the dial in functionality.

The SDK is designed to provision only one device each for either dialing in or out. Once a device is provisioned, subsequent calls to the `usePhoneAudio()` method do not result in additional provisioning.

## Dial-In Attendee Information

To dial-in to the meeting, the user has to know the following dial-in information:

- Dial-In number (US toll by default).
- Global call-in numbers (for non-US attendees).
- Access Code.
- Attendee ID.

The first three can be easily obtained after calling the `meeting.usePhoneAudio()` API as follows:

```js
await meeting.usePhoneAudio();
const accessCode = meeting.meetingInfo.audio.accessCode;
const globalCallInWebUrl = meeting.meetingInfo.audio.globalCallinNumberWebLink;
const tollCallInLabel = meeting.meetingInfo.audio.tollCallInLabel;
const tollNum = meeting.meetingInfo.audio.tollNum;
```

However, to obtain the attendee ID, the easiest way is to listen to the following event:

```js
meeting.on(
    "meeting:self:phoneAudioUpdate",
    (payload) => {
        console.log(payload)
        // payload.dialIn = {
        //     "status": "JOINED",
        //     "attendeeId": "123456"
        // }
    }
);
await meeting.usePhoneAudio();
```

Here's a full code that can be useful:

```js
const dialInInfo = {};
meeting.on(
    "meeting:self:phoneAudioUpdate",
    (payload) => dialInInfo.attendeeId = payload?.dialIn?.attendeeId
);
await meeting.usePhoneAudio();
dialInInfo.accessCode = meeting.meetingInfo.audio.accessCode;
dialInInfo.globalCallInWebUrl = meeting.meetingInfo.audio.globalCallinNumberWebLink;
dialInInfo.tollCallInLabel = meeting.meetingInfo.audio.tollCallInLabel;
dialInInfo.tollNum = meeting.meetingInfo.audio.tollNum;
```

Once you have this information, you can display it to your user for them to dial-in to the meeting via a PSTN call.

After the `usePhoneAudio()` method successfully completes, the user is connected to the meeting through both the browser and the dial-in/dial-out device. Consequently, the next step involves updating the `Meeting` object to disable sending and receiving audio via the browser.

### SDK 3.x:

For 3.x SDKs to disable sending and receiving audio via the browser, send the flag `audioEnabled: false` in the `Meeting` object's [updateMedia](https://webex.github.io/webex-js-sdk/api/#meetingupdatemedia) method:

```js
await meeting.updateMedia({
  audioEnabled: false
});
```



|                  |           |
| ---------------- | --------- |
| **Asynchronous** | Yes       |
| **Parameters**   | `options`   |
| **Returns**      | `Promise<undefined>` |

#### updateMedia Options



| **Name** | **Description** |
| --- | --- |
| `audioEnabled` | (Optional) Toggles receiving and sending of main audio in a meeting. |
| `videoEnabled` | (Optional) Toggles receiving and sending of main video in a meeting. |
| `shareEnabled` | (Optional) Toggles screen sharing. |

### SDK 2.x

For the 2.x SDK to disable sending and receiving audio via the browser, send the flags `sendAudio: false` and `receiveAudio: false` as well as the `Stream` object to the `Meeting` object's [updateAudio](https://webex.github.io/webex-js-sdk/api/#meetingupdateaudio) method:

```js
await meeting.updateAudio({
  sendAudio: false,
  receiveAudio: false,
  stream
});
```



|                  |           |
| ---------------- | --------- |
| **Asynchronous** | Yes       |
| **Parameters**   | `options`   |
| **Returns**      | `Promise<undefined>` |

**Options**



| **Name** | **Description** |
| --- | --- |
| `sendAudio` | **Boolean** - Toggle audio input. |
| `receiveAudio` | **Boolean** - Toggle audio output. |
| `stream` | **Media Stream** - Stream containing the audio track you want to update. |

## Disconnect Dial In or Out Calls

Disconnect dial-in or dial-out calls using the `Meeting` object's [disconnectPhoneAudio](https://webex.github.io/webex-js-sdk/api/#meetingdisconnectphoneaudio) method:

```js
await meeting.disconnectPhoneAudio();
```



|  |  |
| --- | --- |
| **Asynchronous** | Yes |
| **Parameters** | None |
| **Returns** | `Promise` Resolves once the phone audio disconnection has been completed. |

## Re-enable Browser Audio

If, after disconnecting the phone audio for a meeting, you want to enable computer audio (assuming it was not already enabled or was disconnected during the use of phone audio), depending on the SDK version:

### SDK 3.x

For 3.x SDKs to enable sending and receiving audio via the browser, send the flag `audioEnabled: true` in the `Meeting` object's [updateMedia](https://webex.github.io/webex-js-sdk/api/#meetingupdatemedia) method:

```js
await meeting.updateMedia({
  audioEnabled: true
});
```

### SDK 2.x

For the 2.x SDK to enable sending and receiving audio via the browser, send the flags `sendAudio: true` and `receiveAudio: true` as well as the `Stream` object to the `Meeting` object's [updateAudio](https://webex.github.io/webex-js-sdk/api/#meetingupdateaudio) method:

```js
await meeting.updateAudio({
  sendAudio: true,
  receiveAudio: true,
  stream
});
```

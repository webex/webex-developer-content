---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Dial-In Attendee Information
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

When connected to a meeting, the following dialing capabilities are available:

- **Dial out**: Allows the system to call a user's phone, enabling it to be used as the audio input/output device for the meeting.
- **Dial in**: Permits users to call into Webex and use their phone as the meeting's audio input/output device.

<br/>

The SDK also provides functionality to remotely end phone calls in both of the above scenarios.

## Selected section

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

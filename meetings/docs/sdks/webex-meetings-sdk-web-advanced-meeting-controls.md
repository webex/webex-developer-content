---
type: Guide
title: Web Meetings SDK | Advanced Meeting Controls
display_title: Advanced Controls
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls)

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Available Controls

The following advanced meeting controls are available:

- Screen recording
- Lock and unlock meetings
- Send DTMF tones
- Transcription
- Access PSTN phone audio
- Effects for audio and video.
- SIP Call Out and Cancel Calling Out a Participant

## Screen Recording

Once a meeting is [created](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction#create-a-meeting) and [joined](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting), the screen recording controls can be initialized. Only the host of a meeting has the capability to record the screen and manage its controls. Scroll to the end of this page to learn how to determine the current user's role.

### Start a Recording

To start a recording, use the `Meeting` object's `startRecording()` method:

```javascript
await meeting.startRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Pause a Recording

For a recording in process, pause the recording using the `Meeting` object's `pauseRecording()` method:

```javascript
await meeting.pauseRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Resume a Recording

To resume recording, use the `Meeting` object's `resumeRecording()` method:

```javascript
await meeting.resumeRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Stop a Recording

To stop recording, use the `Meeting` object's `stopRecording()` method:

```javascript
await meeting.stopRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

## Lock and Unlock Meetings

When you lock a meeting, no other participants can join unless you admit them. Only the host of a meeting can lock and unlock meetings.

### Lock a Meeting

To lock a meeting, use the `Meeting` object's `lockMeeting()` method:

```javascript
await meeting.lockMeeting();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Unlocking a meeting

To unlock a meeting, use the `Meeting` object's `unlockMeeting()` method:

```javascript
await meeting.unlockMeeting();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | Promise<undefined> |

## Send DTMF Tones

To send DTMF tones in a meeting, use the `Meeting` object's `sendDTMF()` method and pass it a string representing the tone you want to send:

```javascript
await meeting.sendDTMF(DTMFStringToBeSent);
```



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Asynchronous</strong></td>
      <td>Yes</td>
    </tr>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th><strong>Sl. No</strong></th>
                <th colspan="1"><strong>Parameter Name</strong></th>
                <th><strong>Parameter Type</strong></th>
                <th><strong>Mandatory</strong></th>
                <th><strong>Description</strong></th>
              </tr>
              <tr>
                <td>1</td>
                <td><code>DTMFStringToBeSent</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>A string representing the DTMF tone to be sent. Allowed values are 0-9, * and #.</p></td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td><strong>Returns</strong></td>
      <td><code>Promise&lt;undefined&gt;</code></td>
    </tr>
  </tbody>
</table>

## SIP Call Out

To call out a SIP participant to a meeting, use the `Meeting` object's `sipCallOut()` method and pass the SIP address and display name of the participant you want to call.

```javascript
await meeting.sipCallOut(address, displayName);
```



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Asynchronous</strong></td>
      <td>Yes</td>
    </tr>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th><strong>Sl. No</strong></th>
                <th colspan="1"><strong>Parameter Name</strong></th>
                <th><strong>Parameter Type</strong></th>
                <th><strong>Mandatory</strong></th>
                <th><strong>Description</strong></th>
              </tr>
              <tr>
                <td>1</td>
                <td><code>address</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>The SIP address of the invited SIP participant.</p></td>
              </tr>
              <tr>
                <td>2</td>
                <td><code>DisplayName</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>The display name of the invited SIP participant.</p></td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td><strong>Returns</strong></td>
      <td><code>Promise&lt;Object&gt;</code> - Returns an object containing participant details:
        <pre>
          <code>
            {
              "participantId":"abc123-def456-ghi789",
              "address": "sip:user@example.com",
              "displayName": "John Doe",
              "status": "pending"
            }
          </code>
        </pre>
      </td>
    </tr>
  </tbody>
</table>



> **Info**
>
> NOTE: The participant list is not automatically updated when a SIP call-out is initiated. You must save the `participantId` returned by this method to use with `cancelSipCallOut()` if you need to cancel the call-out later. To track when a SIP participant actually joins the meeting after the call-out, listen to the `members:update` event, which provides details about new participants joining the meeting.



## Cancel Calling Out a SIP Participant

To cancel an ongoing SIP call-out, use the `Meeting` object's `cancelSipCallOut()` method and pass the ID of the participant whose call-out you wish to cancel.

```javascript
await meeting.cancelSipCallOut(participantId);
```



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Asynchronous</strong></td>
      <td>Yes</td>
    </tr>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th><strong>Sl. No</strong></th>
                <th colspan="1"><strong>Parameter Name</strong></th>
                <th><strong>Parameter Type</strong></th>
                <th><strong>Mandatory</strong></th>
                <th><strong>Description</strong></th>
              </tr>
              <tr>
                <td>1</td>
                <td><code>participantId</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>The ID of the participant returned by the `sipCallOut` method whose SIP call-out should be cancelled.</p>
                </td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td><strong>Returns</strong></td>
      <td><code>Promise&lt;undefined&gt;</code></td>
    </tr>
  </tbody>
</table>

## Transcription

The basic steps for enabling and processing meeting transcriptions are:

1. Initialize the `Webex` object with a `enableAutomaticLLM` meeting configuration.
1. Enabled the Webex assistant when it is scheduled using the `/meeting` REST API [here](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting).
1. Add users to the meeting.

### Establish a Transcription Socket Connection

When a user initializes the `Webex` object with `enableAutomaticLLM` set to `true`, the Webex Meetings SDK will automatically establish a socket connection between the browser and the transcription backend:

```javascript
webex.init({
    meetings: {
       enableAutomaticLLM: true
    }
});
```

### Listen for the Transcription Connected Event

Listen for the `meeting:transcription:connected` event to determine if the socket connection has been successfully established:

```javascript
meeting.on('meeting:transcription:connected', () => {
    console.log('Transcription Websocket is connected');
});
```

When the event is received, your app can enable transcription.

### Enable Transcription

To start receiving transcriptions during a meeting use the `Meeting` object's `startTranscription()` method with an optional `options` parameter:

```javascript
await meeting.startTranscription(options);
```



| **Parameter Name** | **Description**                                               | **Required** | **Sample value**         | **Type**   |
|----------------|-------------------------------------------------------------------|----------|------------------------------|--------|
| `options`        | Configuration object to be provided while starting transcription. | No       | `{ spokenLanguage?: String}` | Object |



> **Info**
>
> To specify a spoken language in the options, use the language codes conforming with [ISO 639 language code specification](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes).



### Set Caption & Spoken Languages

When you start the transcription, you'll receive a `meeting:receiveTranscription:started` event with a payload containing a list of supported spoken and caption languages:

```javascript
meeting.on('meeting:receiveTranscription:started', (payload) => {
      console.log(payload.captionLanguages);
      console.log(payload.spokenLanguages);
});
```

The `captionLanguages` and `spokenLanguages` arrays contain the language code for the supported languages. The language codes conform with the [ISO 639 language code specification](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes).

### Start Receiving Transcription

To receive transcriptions, listen for the `meeting:caption-received` event which contains the captions generated from the meeting's audio:

```javascript
meeting.on('meeting:caption-received', (payload) => {
      //use payload to display captions
});
```

Here's an example of the a transcription payload:

```javascript
{
    "captions": [
        {
            "id": "88e1b0c9-7483-b865-f0bd-a685a5234943",
            "isFinal": true,
            "text": "Hey, everyone.",
            "currentSpokenLanguage": "en",
            "timestamp": "1:22",
            "speaker": {
                "speakerId": "8093d335-9b96-4f9d-a6b2-7293423be88a",
                "name": "Name"
            }
        },
        {
            "id": "e8fd9c60-1782-60c0-92e5-d5b22c80df2b",
            "isFinal": true,
            "text": "That's awesome.",
            "currentSpokenLanguage": "en",
            "timestamp": "1:26",
            "speaker": {
                "speakerId": "8093d335-9b96-4f9d-a6b2-7293423be88a",
                "name": "Name"
            }
        },
        {
            "id": "be398e11-cf08-92e7-a42d-077ecd60aeea",
            "isFinal": true,
            "text": "आपका नाम क्या है?",
            "currentSpokenLanguage": "hi",
            "timestamp": "1:55",
            "speaker": {
                "speakerId": "8093d335-9b96-4f9d-a6b2-7293423be88a",
                "name": "Name"
            }
        },
        {
            "id": "84adc1a7-b3c3-5a49-0588-aa787b1437eb",
            "isFinal": true,
            "translations": {
                "en": "What is your name?"
            },
            "text": "आपका नाम क्या है?",
            "currentSpokenLanguage": "hi",
            "timestamp": "2:11",
            "speaker": {
                "speakerId": "8093d335-9b96-4f9d-a6b2-7293423be88a",
                "name": "Name"
            }
        },
        {
            "id": "84c89387-cd5d-ce15-1867-562c0a91155f",
            "isFinal": true,
            "translations": {
                "hi": "तुम्हारा नाम क्या है?"
            },
            "text": "What's your name?",
            "currentSpokenLanguage": "en",
            "timestamp": "2:46",
            "speaker": {
                "speakerId": "8093d335-9b96-4f9d-a6b2-7293423be88a",
                "name": "Name"
            }
        }
    ],
    "interimCaptions": {
        "88e1b0c9-7483-b865-f0bd-a685a5234943": [],
        "e8fd9c60-1782-60c0-92e5-d5b22c80df2b": [],
        "be398e11-cf08-92e7-a42d-077ecd60aeea": [],
        "84adc1a7-b3c3-5a49-0588-aa787b1437eb": [],
        "84c89387-cd5d-ce15-1867-562c0a91155f": []
    }
}
```

### Change the Spoken Language

During the meeting, if you'd like to change the spoken language, use the `Meeting` object's `setSpokenLanguage()` method:

```javascript
const currentSpokenLanguage = await meeting.setSpokenLanguage(selectedLanguage);
```

Choose the `selectedLanguage` when you start the transcription. If you select the spoken language and speak in that language, the system displays the caption in the same language. If you set the caption language to a different language at any point, a user speaking in this new language will see the caption in that different language.

### Change the Caption Language

During the meeting, use the `Meeting` object's `setCaptionLanguage()` method to set the caption language:

```javascript
const currentCaptionLanguage = await meeting.setCaptionLanguage(selectedLanguage);
```

You'll choose the `selectedLanguage` language code at the start of the transcription. The system translates any speech, no matter the language, into this selected language.



> **Info**
>
> Any participant can choose the caption language, but only the meeting host can set the spoken language. After setting a spoken language, the Webex cloud expects and assumes that all participants will communicate in that language.



### Stop Receiving Transcription

To stop receiving the transcriptions, use the `Meeting` object's `stopTranscription()` method:

```javascript
meeting.stopTranscription();
```

## Use PSTN Phone Audio

In a meeting, if the audio isn't clear or there are issues using device audio (desktop app, mobile app, or web app), Webex lets you dial in to a meeting via PSTN. The following controls are available:

- Use Phone Audio
- Disconnect Phone Audio

For more information see [Use PSTN Phone Audio for Meetings](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting)

## Effects: Meeting Audio and Video

Webex meetings support the following three effects:

- Background noise removal (BNR) for Webex audio.
- Background blur for Webex video.
- Virtual backgrounds for Webex video.

For more information, see [Meeting Audio & Video Effects](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects).

## Determining the Current User's Role

### The `getCurUserType` API

This document highlights that certain controls are reserved for the meeting host. To find out the current user's role, use the following method:

```javascript
const userType = meeting.getCurUserType();
```

This method provides a string that specifies the user's role, which could be:

- `host`
- `cohost`
- `panelist`
- `attendee`

### Event for Real-Time Role Updates

While the `getCurUserType` API provides the current user type, the SDK also emits an event to notify of any role changes in real-time:

```javascript
meeting.on("meeting:self:rolesChanged", (payload) => {
  // Handle the role change
  // Example Payload: When an Attendee is made host
  // {
  //   "payload": {
  //       "oldRoles": [
  //           "ATTENDEE"
  //       ],
  //       "newRoles": [
  //           "MODERATOR",
  //           "ATTENDEE"
  //       ]
  //   }
  // }
});
```

The payload from this event contains the updated role information. The `getCurUserType` API will also return the correct role when called within the callback of this event.

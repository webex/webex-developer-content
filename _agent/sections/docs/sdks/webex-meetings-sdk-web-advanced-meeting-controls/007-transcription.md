---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Transcription
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Selected section

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

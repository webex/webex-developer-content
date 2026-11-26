---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Fetch a Voicemail Transcription
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-voicemail.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `VoicemailClient` object is a supplementary Calling SDK module that adds comprehensive support for voicemail functionality. 

---

Before continuing, refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how `Call` objects are created and how different modules are instantiated. The `VoicemailClient` object offers a variety of functions which are covered in this article in detail.

## Selected section

## Fetch a Voicemail Transcription

The `getVMTranscript()` method API fetches a transcript for a voicemail. It takes a `messageID` as an argument:

```javascript
const voicemailTranscriptResponse = await voicemailClient.getVMTranscript(messageID);
```



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | messageID\<string\>               |
| Returns    | Promise\<VoicemailResponseEvent\> |

Here's an example of the response received when a transcript is fetched successfully:

```javascript
{
 statusCode: 200,
    data: {
  transcript: "This is some transcript text from the voicemail ID.",
 },
    message: READY | FAILURE | NA | PENDING,
};
```



> **Info**
>
> The transcript object populates the string only when the transcription is complete and `READY`. `FAILURE` indicates that the voicemail service was unable to transcribe the voicemail, while `PENDING` indicates that transcription is in progress. `NA` indicates that transcription is not enabled for the user's voicemails.



Here's an example of a `messageID` returned by the voicemail client:

```javascript
v2.0/user/69fde5ad-fb8b-4a1b-9998-b0999e95719b/VoiceMessagingMessages/dfe55899-1f55-474f-8f00-bc5915757070
```



> **Info**
>
> The entire string is used as the ID.



### Mark a Voicemail As Read

The `voicemailMarkAsRead()` method API marks a voicemail as read. It takes a `messageID` as an argument:

```javascript
const voicemailMarkAsReadResponse = await voicemailClient.voicemailMarkAsRead(messageID);
```



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | messageID\<string\>               |
| Returns    | Promise\<VoicemailResponseEvent\> |

Here's an example response from the `voicemailMarkAsRead()` method:

```javascript
{
 statusCode: 200,
    data: {},
    message: SUCCESS,
};
```

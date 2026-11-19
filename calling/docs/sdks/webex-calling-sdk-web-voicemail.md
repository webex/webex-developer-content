---
type: Guide
title: Web Calling SDK | Voicemail
display_title: Voicemail
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail)

The `VoicemailClient` object is a supplementary Calling SDK module that adds comprehensive support for voicemail functionality. 

---

Before continuing, refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how `Call` objects are created and how different modules are instantiated. The `VoicemailClient` object offers a variety of functions which are covered in this article in detail.

## Initialize the voicemailClient

The `VoicemailClient` is implemented as the `Voicemail` class in the SDK and there are two ways of instantiating it.

To instantiate just the `VoicemailClient`, use the `createVoicemailClient` method:

```javascript
const voicemailClient = createVoicemailClient(webex, logger);
```

If the `VoicemailClient` is instantiated through the `calling` instantiation:

```javascript
const voicemailClient = calling.voicemailClient;
```

The voicemail client instance must be initialized to enable access to the voicemail backend services using the `init()` methood of the `voicemailClient` object:

```javascript
const initResponse = await voicemailClient.init();
```

## Voicemail Response Object

Here's an example response from the voicemailClient method:

```javascript
{
  statusCode: number;
  data: {
    voicemailList?: MessageInfo[];
    voicemailContent?: {
      type: string | null;
      content: string | null;
    };
    voicemailSummary?: SummaryInfo;
    voicemailTranscript?: string | null;
    error?: string;
  };
  message: string | null;
};
```

### Fetch a Voicemail List

The `getVoicemailList()` method retrieves the voicemails present in the voicemail box of the user:

```javascript
const voicemailListResponse = await voicemailClient.getVoicemailList(
  OFFSET,
  OFFSETLIMIT,
  SORT.DESC,
  true
);
```

The following table describes the options available for the arguments passed to the `getVoicemailList()` method:



<table>
  <colgroup>
    <col style="width: 12%" />
    <col style="width: 88%" />
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        <p>Options</p>
        
          <table>
            <tbody>
              <tr>
                <th colspan="1"><strong>Name</strong></th>
                <th colspan="1"><strong>Description</strong></th>
                <th colspan="1"><strong>Values</strong></th>
                <th colspan="1"><strong>Required</strong></th>
              </tr>
              <tr>
                <td><code>sort</code></td>
                <td>
                  Sorting order of voicemail list, ASC or DESC.
                </td>
                <td>
                  <p>
                    <em><strong>String</strong></em>
                  </p>
                  
                    <table>
                      <tbody>
                        <tr>
                          <td>
                            <strong>ASC</strong>
                          </td>
                          <td>
                            <strong>DESC</strong>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>yes</td>
              </tr>
              <tr>
                <td><code>offset</code></td>
                <td>
                  Number of records to skip.
                </td>
                <td>
                  <p>
                    <strong>Number</strong>
                </td>
                <td>yes</td>
              </tr>
              <tr>
                <td><code>offsetLimit</code></td>
                <td>
                  Index of the voicemail to fetch from the voicemail list.
                </td>
                <td>
                  <strong>String</strong>
                </td>
                <td>yes</td>
              </tr>
              <tr>
                <td colspan="1"><code>refresh</code></td>
                <td colspan="1">
                  Refresh the list of voicemails from the backend.
                </td>
                <td colspan="1">
                  <strong>Boolean</strong>
                </td>
                <td colspan="1">yes</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
  </tbody>
</table>



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | See table above                   |
| Returns    | Promise\<VoicemailResponseEvent\> |

## Fetch a Voicemail Summary

The `getVoicemailSummary()` method fetches the count for various categories of voicemails in a user's mailbox. The method's response consists of counts for new voicemails received, new urgent voicemails received, old voicemails, and old urgent voicemails:

```javascript
const voicemailSummaryResponse = await voicemailClient.getVoicemailSummary();
```



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | --                                |
| Returns    | Promise\<VoicemailResponseEvent\> |

Here's an example of the response for the `getVoicemailSummary()` method:

```javascript
{
 statusCode: 200,
    data: {
     voicemailSummary: {
         newMessages: 2,
         newUrgentMessages: 1,
         oldMessages: 3,
         oldUrgentMessages: 2,
        },
 },
    message: SUCCESS,
};
```

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

## Mark a Voicemail As Unread

The `voicemailMarkAsUnread()` method API marks a voicemail as unread. It takes a `messageID` as an argument:

```javascript
const voicemailMarkAsUnreadResponse =
  await voicemailClient.voicemailMarkAsUnread(messageID);
```



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | messageID\<string\>               |
| Returns    | Promise\<VoicemailResponseEvent\> |

Here's an example response from the `voicemailMarkAsUnread()` method:

```javascript
{
 statusCode: 200,
    data: {},
    message: SUCCESS,
};
```

## Delete a Voicemail

The `deleteVoicemail()` deletes a voicemail. It takes a `messageID` as an argument:

```javascript
const voicemailDeleteResponse = await voicemailClient.deleteVoicemail(messageID);
```



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | messageID\<string\>               |
| Returns    | Promise\<VoicemailResponseEvent\> |

Here's an example response from the `deleteVoicemail()` method upon successfully deleting a voicemail:

```javascript
{
    statusCode: 200,
    data: {},
    message: SUCCESS,
};
```

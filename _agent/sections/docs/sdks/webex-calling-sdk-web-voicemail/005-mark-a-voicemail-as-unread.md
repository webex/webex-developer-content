---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Mark a Voicemail As Unread
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-voicemail.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `VoicemailClient` object is a supplementary Calling SDK module that adds comprehensive support for voicemail functionality. 

---

Before continuing, refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how `Call` objects are created and how different modules are instantiated. The `VoicemailClient` object offers a variety of functions which are covered in this article in detail.

## Selected section

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

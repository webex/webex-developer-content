---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Fetch a Voicemail Summary
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-voicemail.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `VoicemailClient` object is a supplementary Calling SDK module that adds comprehensive support for voicemail functionality. 

---

Before continuing, refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how `Call` objects are created and how different modules are instantiated. The `VoicemailClient` object offers a variety of functions which are covered in this article in detail.

## Selected section

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

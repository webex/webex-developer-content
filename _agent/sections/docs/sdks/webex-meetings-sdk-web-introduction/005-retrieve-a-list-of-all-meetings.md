---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Retrieve a List of All Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

## Retrieve a List of All Meetings

You can create more than one meeting at a time. To obtain a list of all current meetings, use the `Meetings` object's `getAllMeetings()` method:

```js
const meetingList = webex.meetings.getAllMeetings();
```



|              |                          |
| ------------ | ------------------------ |
| Asynchronous | No                       |
| Parameters   | No parameters required   |
| Returns      | Map\<MeetingId,Meeting\> |

Here's an example of a returned list of meetings:

```json
{
  "3c9628aa-b51d-45c4-9166-1b9f7dafe95e" : { id: "3c9628aa-b51d-45c4-9166-1b9f7dafe95e", ...otherMeetingObjectAttributes },
  "c7d69b95-c9c6-40c1-9138-c6005b8be554": { id: "c7d69b95-c9c6-40c1-9138-c6005b8be554", ...otherMeetingObjectAttributesAndMethods },
}
```

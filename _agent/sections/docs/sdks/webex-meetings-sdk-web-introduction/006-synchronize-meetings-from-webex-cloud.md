---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Synchronize Meetings from Webex Cloud
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Webex Web SDK `meetings` object. It covers multiple methods and events related to meeting creation and retrieval.

## Selected section

## Synchronize Meetings from Webex Cloud

If your application is running on behalf of a registered Webex user, and that user has meetings running, you can use the `Meetings` object's `syncMeetings()` method to synchronize and then retrieve a list of those meetings.

```js
await webex.meetings.syncMeetings();
```



|              |                        |
| ------------ | ---------------------- |
| Asynchronous | Yes                    |
| Parameters   | No parameters required |
| Returns      | Promise\<undefined\>   |

After the `syncMeetings()` call is successful, use the `getAllMeetings` method to retrieve the list of meetings:

```js
await webex.meetings.syncMeetings();
const meetingList = webex.meetings.getAllMeetings();
```

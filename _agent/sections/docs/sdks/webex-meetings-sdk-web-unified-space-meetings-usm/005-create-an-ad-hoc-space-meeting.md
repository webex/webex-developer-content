---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Create an Ad-hoc Space Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for USM](002-prerequisites-for-usm.md)

## Article introduction

Webex Meeting today has three distinct meeting experiences: Personal Meeting Rooms (PMR), Scheduled Meetings, and Space Meetings. Each of those meeting types has distinct experiences. Unified Space Meetings (USM) consolidates the experiences of Space Meetings with Webex Meetings and melds them together.

This article explains how to enable USM, how to start ad-hoc meetings, including information on password and captcha support.

## Selected section

## Create an Ad-hoc Space Meeting

Create an ad-hoc space meeting using a room ID via the Webex REST [Room API](https://developer.webex.com/docs/api/v1/rooms/list-rooms).

Here's a typical room object:

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JPT00vYzVlNjgxODAtMDkxMy0xMWVkLWFmZjQtYTc5YzYwNWU1MEKl",
  "title": "Example Room",
  "type": "group",
  "isLocked": false,
  "lastActivity": "2022-08-25T07:30:18.466Z",
  "creatorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8zNDRlYTE4My05ZDVkLTRlNzctYWVkMi1jNGYwMDRhZmR6NUV",
  "created": "2022-07-21T16:40:04.760Z",
  "ownerId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGVyNHZ",
  "isPublic": false
}
```

Pass the `id` to the `Meetings` object's `create()` method to create a new meeting:

```js
webex.meetings.create(roomId);
```


|     |     |
| --- | --- |
| **Asynchronous** | Yes |
| **Mandatory Parameters** | `roomId` |
| **Returns** | A promise that gets resolved and returns a `Meeting` object. |

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Fetch a Meeting Instance
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-join-a-meeting.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Joining a meeting using the Webex Meetings Web SDK allows you to participate in video conferences. This article guides you through the process of joining a meeting and covers various additional scenarios, including joining with or without media, configuring audio and video settings, and screen sharing.

## Selected section

## Fetch a Meeting Instance

A `meeting` instance is typically created once a meeting is initiated through the SDK. If a meeting has already been created on the SDK, you can retrieve it using the SDK's `meetings` object by passing a `meetingId`.



> **Info**
>
> This method does not fetch the list of all meetings from the Webex cloud. It only lists the meetings that are created either with `webex.meetings.create` or `webex.meetings.syncMeetings`.



```js
const meeting = webex.meetings.getAllMeetings()[meetingId];
```

If participants have already joined the meeting, it can be retrieved from Webex Cloud. Refer to [Sync Meetings](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction#synchronize-meetings-from-webex-cloud).

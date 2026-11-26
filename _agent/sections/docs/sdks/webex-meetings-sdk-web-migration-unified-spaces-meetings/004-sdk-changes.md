---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- SDK Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](011-limitations.md)

## Article introduction

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Selected section

## SDK Changes

Please adhere to the guidelines below to transition from utilizing `roomId/spaceId` to `meetingId/sipUrl` within the SDK.

### Code Changes Required

The support for direct use of `roomId/spaceId` in Webex JS SDK and Meeting Widgets for creation and joining a meeting is being deprecated. You are encouraged to utilize the Meetings API to start an ad-hoc meeting. The Meetings API provides additional flexibility to developers. Once the meeting has been created using a licensed user or service-app, the Webex JS SDK can be utilized to join the meeting.

#### Before...

You'd use code like the following to create a Webex meeting using a specified room ID or space ID:

```javascript
webex.meetings.create('room-id-or-space-id').then((meeting) => {
  console.log(meeting);
});
```

#### After...

1. Create a meeting by calling the API [https://webexapis.com/v1/meetings](https://webexapis.com/v1/meetings) and obtain a `meetingId` or `sipUrl`.

    - Find the full details of the API [here](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting)
    - Read through [Integrations](https://developer.webex.com/docs/integrations) and [Service Apps](https://developer.webex.com/docs/service-apps) to use appropriate access tokens.
2. Check if the improved meeting experience is enabled by checking the configuration of your `webex` object - `webex.meetings.config.experimental.enableUnifiedMeetings`. Toggle the improved meeting experience by setting the above flag to `true` if not already enabled

3. Creating a Webex meeting using either a meeting ID or a SIP URL:

```javascript
webex.meetings.create('meeting-id or sipUrl').then((meeting) => {
  console.log(meeting);
});
```

If a `roomId/spaceId` is specified as the meeting destination, the SDK will generate an error with the code and message below:
**Error Code** - 30105
**Error Message** - 'Using the space ID as a destination is no longer supported. Please refer to the migration section in this document to use the meeting ID or SIP address.



> **Info**
>
> Using **_personId_** to create a meeting is still supported. Please use the type as **'PERSON_ID'**.

---
type: Guide
title: Web Meetings SDK | Unified Space Meetings (USM)
display_title: Unified Space Meetings
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm)

Webex Meeting today has three distinct meeting experiences: Personal Meeting Rooms (PMR), Scheduled Meetings, and Space Meetings. Each of those meeting types has distinct experiences. Unified Space Meetings (USM) consolidates the experiences of Space Meetings with Webex Meetings and melds them together.

This article explains how to enable USM, how to start ad-hoc meetings, including information on password and captcha support.

## Webex Meeting Types

Webex meetings can be broadly classified as:

1. **Webex Meetings**
   1. *Scheduled Webex Meetings* - The meeting is created first and then the meeting information such as the meeting ID, pass code, and unique meeting link is sent to the **invitees**.
   1. *PMR (personal meeting room or "instant meeting")* - A meeting with a static URL that can be attached to a meeting schedule as well as sent out as a message for anyone to join.
1. **Space Meetings**
   1. *Scheduled Space Meetings* - The meeting is created first and then the meeting information such as the meeting ID, pass code, and unique meeting link is sent to the **members of the space**.
   1. *Ad-hoc Space Meetings* - The meeting can be started instantly from a team space, without any pre-scheduled meeting links. Although these meetings are instant and do not have a meeting ID or URL when they're started, Webex creates both which can be obtained via the Meeting Info API.

## Prerequisites for USM

The only prerequisite is that unified meetings must be enabled.

In the SDK, the default values for `enableUnifiedMeetings` and `enableAdhocMeetings` have been set to `true`.

## Verify that USM is Enabled

To verify that USM is enabled, check to see that the following statement returns `true`:

```js
webex.meetings.config.experimental.enableUnifiedMeetings;
```

## Enabled USM if It's Disabled

To toggle USM on or off:

```js
webex.meetings._toggleUnifiedMeetings(changeState);
```



|                  |                                     |
| ---------------- | ----------------------------------- |
| **Asynchronous** | No                                  |
| **Parameters**   | `changeState<Boolean (true / false)>` |
| **Returns**      | undefined                           |

You can also change the configuration by toggling the following values:

```js
Meetings :{
 experimental: {
      enableUnifiedMeetings: false,
      enableAdhocMeetings: false
    }
  }
```

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

## Join an Ad-hoc Meeting in Progress

When an ad-hoc meeting is created, Webex generates a meeting ID and a URL, which then can be shared with others who can then join using that information.

To retrieve that meeting information, access the `Meeting` object's `meetingInfo` instance variable:

```js
meeting.meetingInfo;
```

For a working example, see the [Kitchen Sink App](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/).

## Join a Meeting by Entering a Password/Captcha

If the user is not a member of the space where the has been created, the user is prompted for the meeting password. If the user enters the password incorrectly too many times, captcha information is provided along with an informational error code.

For more information see:

- [Verify a Meeting Password](https://webex.github.io/webex-js-sdk/api/#meetingverifypassword)
- [Password and Captcha Workflow](FIXME/./password-captcha-flow.md)

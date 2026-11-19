---
type: Guide
title: Web Meetings SDK | Migration to Improved Space Meetings
display_title: Migration To Improved Meetings
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings)

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Pre-requisites

Webex JS SDK version 2.60.0 or above.

## Improved meeting experience

Earlier, your experience in a meeting associated with a space was tied to who created the space (known as the meeting sponsor). The feature set available to you depended on the type of account that person had. We’ve removed the concept of meeting sponsorship. Now, only the host's license determines the meeting capabilities. Now, when you join or schedule a meeting in a space, you have access to the features you’ve come to enjoy in Webex Meetings. You can leverage this new experience in every meeting you schedule or join from here on in.

Please refer to this [help article](https://help.webex.com/en-us/article/gxw5jz/Webex-App-%7C-Improved-meetings-associated-with-a-space) for additional details.

## Migration from Spark or Space meeting to the improved meetings experience

The initial stage of transitioning from Space or Spark (hereafter referred to as the classic meeting experience) to the improved meeting experience involves the management of user licenses as the host's license now determines the meeting capabilities.

- Create a [Webex site](https://help.webex.com/en-us/article/naqlzeu/Add-and-manage-a-Webex-site-in-Control-Hub) and re-distribute the licenses among users.
- Create a [Service App](https://developer.webex.com/docs/service-apps) for end-to-end provisioning of users and other features.



> **Info**
>
> As part of the improved experience with space meetings, creating a guest user through [Guest Issuer](https://developer.webex.com/docs/guest-issuer) is being deprecated. Now the way to create a guest user would be through a [Service App](https://developer.webex.com/docs/service-apps) tied to a guest site.



Users with a Webex account can acquire their access token from the [developer portal](https://developer.webex.com/docs/getting-started) by logging in with their authentication details (username and password).

For guest users, an access token can be obtained via a [Service App](https://developer.webex.com/docs/service-apps).

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



## Join the Meeting by Entering a Password or Captcha

If the user is not part of the space where the meeting is created then the user will be prompted for the password. After multiple failed password attempts, captcha information is provided along with the appropriate error code. The user submits the captcha with the password to join the meeting successfully.
For more information, see:

- [Meeting Verify Password](https://webex.github.io/webex-js-sdk/api/#meetingverifypassword)
- [Password captcha flow](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha)

## Make another participant the host

A participant can be made a host using the [transfer](https://webex.github.io/webex-js-sdk/api/#meetingtransfer) method within a meeting object. Only a host can make another participant host. 

Use the following code to transfer host privileges to another participant.

```javascript
meeting.transfer('participant-id');
```



> **Info**
>
> Only an existing host can promote a participant to host.



## Invite another participant

A participant can be invited to the meeting using the [invite](https://webex.github.io/webex-js-sdk/api/#meetinginvite) method within the meeting object. Only a host can invite another participant. Participants can be invited using an email address.

Use the following code to invite another participant to an existing meeting. You can use either the `emailAddress` or the `phoneNumber` parameter.

```javascript
meeting.invite(invitee: {
  emailAddress: 'johndoe@abc.com',
  phoneNumber: '1234',
});
```

To cancel an outgoing phone invite, use the following method.

```javascript
meeting.cancelPhoneInvite(invitee: {
  phoneNumber: '1234',
});
```

## Reclaim the host role

A participant can reclaim host privileges in the meeting by using the [assignRoles](https://webex.github.io/webex-js-sdk/api/#membersassignroles) method within the members object. The code snippet below illustrates its use.

```javascript
  const selfId = meeting.members.selfId;
  const role = {
    type: 'MODERATOR',
    hasRole: true,
    hostKey,
  };

  meeting.members.assignRoles(selfId, [role])
```

## Meeting Widget changes

Please adhere to the guidelines below to transition from utilizing `roomId/spaceId` to `meetingId/sipUrl` within the Meetings Widget.

### Before...

You'd use code like the following to create a Webex meeting widget using a specified room ID or space ID:

```javascript
import { WebexMeetingsWidget } from '@webex/widgets';

import '@webex/widgets/dist/css/webex-widgets.css';

export default function App() {
  return (
    <WebexMeetingsWidget
      style={{ width: '1000px', height: '500px' }} // Substitute with any arbitrary size or use `className`
      accessToken='<ACCESS_TOKEN>'
      meetingDestination='<ROOM_ID>' // NOTICE THIS LINE
    />
  );
}
```

### After...

1. Use **step-1** from [SDK Changes](#sdk-changes) to obtain `meetingId` or `sipUrl`.

2. The code snippet below illustrates the process of creating a Webex meeting using either a meeting ID or a SIP URL:

```javascript
import { WebexMeetingsWidget } from '@webex/widgets';

import '@webex/widgets/dist/css/webex-widgets.css';

export default function App() {
  return (
    <WebexMeetingsWidget
      style={{ width: '1000px', height: '500px' }} // Substitute with any arbitrary size or use `className`
      accessToken='<ACCESS_TOKEN>'
      meetingDestination='<MEETING_ID OR SIP_URL>' // NOTICE THIS LINE
    />
  );
}
```



> **Info**
>
> If `spaceId` is passed for `meetingDestination` the widget will throw an error.



## Space/Recent Widgets Changes

In this context, you cannot choose the ID for creating or joining a meeting, so we won't be addressing the deprecation of the `roomId`. Given that the improved meeting experience mandates a license for each user to participate in meetings, the meet button will be rendered inactive for users without a valid license.

Please refer to the initial section in this document to distribute licenses among users.

## Limitations

- Limitations for consumer organization users. In the improved meeting experience associated with new spaces, Gmail users can initiate scheduled or instant meetings, while in the classic meeting experience, neither old nor new Gmail users can start scheduled or instant meetings.

- Limitation in the Webex App: individuals not listed as invitees will be placed in the lobby and require admission.

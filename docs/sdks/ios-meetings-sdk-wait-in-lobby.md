---
type: Guide
title: iOS Meetings SDK | Wait in Lobby
display_title: Wait in Lobby
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-wait-in-lobby
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-wait-in-lobby)

When joining a meeting through the SDK, attendees might be required to wait in a virtual lobby. The lobby serves as a holding area where participants can be screened before joining the actual meeting or wait for the meeting to commence.

---

This article will show you how to handle the various lobby functions supported by the iOS Meetings SDK.

## Scenarios Requiring Lobby Wait

Attendees may be asked to wait in the lobby under the following circumstances:

- They are not included in the calendar invitation.
- They are attempting to join a locked Webex scheduled meeting or Webex Personal Room meeting.
- They are trying to join a Webex team meeting but are either not members of the team space or do not possess Webex Teams accounts.

### Waiting in the Lobby Callback

When an attendee is placed in the lobby, the `call.onWaiting` callback is triggered. This callback provides the reason why the attendee is required to wait:

```swift
call.onWaiting = {reason in
  ...
}
```

### Entering the Meeting from the Lobby Callback

Once attendees are allowed to join the meeting from the lobby, the `call.onConnected` callback is triggered, indicating that the attendee has successfully entered the meeting.

```swift
call.onConnected = {
  ...
}
```

### Host Notifications and Actions Callback

For the meeting host, the arrival of an attendee in the lobby triggers the `onCallMembershipChanged` callback with the `CallMembershipChangedEvent.waiting` event. The host can then allow the attendee into the meeting using the `call.letIn` method:

```swift
call.letIn([membership], completionHandler: { (error) in
  ...
})
```

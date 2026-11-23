---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Determining the Current User's Role
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Selected section

## Determining the Current User's Role

### The `getCurUserType` API

This document highlights that certain controls are reserved for the meeting host. To find out the current user's role, use the following method:

```javascript
const userType = meeting.getCurUserType();
```

This method provides a string that specifies the user's role, which could be:

- `host`
- `cohost`
- `panelist`
- `attendee`

### Event for Real-Time Role Updates

While the `getCurUserType` API provides the current user type, the SDK also emits an event to notify of any role changes in real-time:

```javascript
meeting.on("meeting:self:rolesChanged", (payload) => {
  // Handle the role change
  // Example Payload: When an Attendee is made host
  // {
  //   "payload": {
  //       "oldRoles": [
  //           "ATTENDEE"
  //       ],
  //       "newRoles": [
  //           "MODERATOR",
  //           "ATTENDEE"
  //       ]
  //   }
  // }
});
```

The payload from this event contains the updated role information. The `getCurUserType` API will also return the correct role when called within the callback of this event.

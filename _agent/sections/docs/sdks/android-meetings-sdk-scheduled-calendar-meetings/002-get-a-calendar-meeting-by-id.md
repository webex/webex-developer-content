---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Get a Calendar Meeting by ID
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-scheduled-calendar-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the Calendar meeting APIs available in the SDK and their usage.

---

Calendar meeting APIs are intended to manage and interact with scheduled meetings within the application. These are not applicable for Guest Users.

## Selected section

## Get a Calendar Meeting by ID

To retrieve a calendar meeting using its ID:

```kotlin
getById(meetingId: String, CompletionHandler<CalendarMeeting>())
```

### getById() Method Parameters

* `meetingId`: The identifier of the meeting.
* `completionHandler`: A callback that returns the `CalendarMeeting` object corresponding to the `meetingId`.

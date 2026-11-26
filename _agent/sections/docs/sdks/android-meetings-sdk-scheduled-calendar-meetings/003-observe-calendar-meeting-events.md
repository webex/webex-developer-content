---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Observe Calendar Meeting Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-scheduled-calendar-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the Calendar meeting APIs available in the SDK and their usage.

---

Calendar meeting APIs are intended to manage and interact with scheduled meetings within the application. These are not applicable for Guest Users.

## Selected section

## Observe Calendar Meeting Events

Set an observer to listen for calendar meeting events:

```kotlin
fun setObserver(observer: CalendarMeetingObserver?)
```

The observer listens for the following events:

* `CalendarMeetingAdded`: Triggered when a new calendar meeting is created.
* `CalendarMeetingUpdated`: Triggered when an existing calendar meeting is updated (for example, a title change).
* `CalendarMeetingRemoved`: Triggered when a calendar meeting is deleted

---
type: Guide
title: Android Meetings SDK | Scheduled Calendar Meetings
display_title: Scheduled Calendar Meetings
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings)

This article outlines the Calendar meeting APIs available in the SDK and their usage.

---

Calendar meeting APIs are intended to manage and interact with scheduled meetings within the application. These are not applicable for Guest Users.

## Retrieve Scheduled Meetings

To fetch a list of scheduled meetings, use the `list()` method with date filters:

```kotlin
list(fromDate: Date?, toDate: Date?, CompletionHandler<List<CalendarMeeting>>())
```

### list() Method Parameters

* `fromDate`: A `Date` parameter to filter meetings ending on or after this date. If `null`, it defaults to 7 days before the current date.
* `toDate`: A `Date` parameter to filter meetings starting on or before this date. If `null`, it defaults to 30 days after the current date.
* `completionHandler`: A callback that returns a list of `CalendarMeeting` objects.



> **Info**
>
> The `list()` method retrieves meetings scheduled within a range from 7 days in the past to 30 days in the future from the current date.



### Retrieval Example

Consider a scenario where the user has multiple meetings scheduled for the current day:

* Meeting 1: 1:00 PM to 2:00 PM
* Meeting 2: 1:15 PM to 1:45 PM
* Meeting 3: 1:30 PM to 2:30 PM
* Meeting 4: 3:00 PM to 3:30 PM
* Meeting 5: 3:30 PM to 5:00 PM

If `fromDate` and `toDate` are set between 2:00 PM and 3:00 PM, the `list` API will return Meeting 1, Meeting 3, and Meeting 4.

## Get a Calendar Meeting by ID

To retrieve a calendar meeting using its ID:

```kotlin
getById(meetingId: String, CompletionHandler<CalendarMeeting>())
```

### getById() Method Parameters

* `meetingId`: The identifier of the meeting.
* `completionHandler`: A callback that returns the `CalendarMeeting` object corresponding to the `meetingId`.

## Observe Calendar Meeting Events

Set an observer to listen for calendar meeting events:

```kotlin
fun setObserver(observer: CalendarMeetingObserver?)
```

The observer listens for the following events:

* `CalendarMeetingAdded`: Triggered when a new calendar meeting is created.
* `CalendarMeetingUpdated`: Triggered when an existing calendar meeting is updated (for example, a title change).
* `CalendarMeetingRemoved`: Triggered when a calendar meeting is deleted

## The canJoin Attribute

The `canJoin` boolean attribute in `CalendarMeeting` indicates whether a meeting is ready to be joined or started. It is set to `true` shortly before a meeting's start time and during an ongoing meeting. Once a meeting ends, a `CalendarMeetingUpdated` event is fired with `canJoin` set to `false`. The `canJoin` attribute is set to `true` when a meeting can be started or when the SDK is initialized and a meeting is already in progress.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Retrieve Scheduled Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-scheduled-calendar-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the Calendar meeting APIs available in the SDK and their usage.

---

Calendar meeting APIs are intended to manage and interact with scheduled meetings within the application. These are not applicable for Guest Users.

## Selected section

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

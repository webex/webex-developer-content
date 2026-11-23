---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- The canJoin Attribute
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-scheduled-calendar-meetings). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-scheduled-calendar-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the Calendar meeting APIs available in the SDK and their usage.

---

Calendar meeting APIs are intended to manage and interact with scheduled meetings within the application. These are not applicable for Guest Users.

## Selected section

## The canJoin Attribute

The `canJoin` boolean attribute in `CalendarMeeting` indicates whether a meeting is ready to be joined or started. It is set to `true` shortly before a meeting's start time and during an ongoing meeting. Once a meeting ends, a `CalendarMeetingUpdated` event is fired with `canJoin` set to `false`. The `canJoin` attribute is set to `true` when a meeting can be started or when the SDK is initialized and a meeting is already in progress.

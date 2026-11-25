---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Meeting Series, Scheduled Meetings, and Meeting Instances
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Meeting Series, Scheduled Meetings, and Meeting Instances

When using the [Meetings](https://developer.webex.com/docs/api/v1/meetings) and [Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees) API resources, it's important to understand the difference between "meeting series", "scheduled meetings", and "meetings" objects. Each of these objects may be sent to or received from the API. To differentiate them, the value of the `meetingType` attribute in the object will be one of:

* `meetingSeries` – a container object that includes all of the scheduling information for a meeting
* `scheduledMeeting` – an object that represents the information associated with the scheduling information associated with a single instance of a meeting; a scheduledMeeting object can be thought of as a “child” of a meetingSeries object
* `meeting` – an object that represents a meeting that is currently happening or has happened in the past; this object is created only when a meeting starts

Both meeting series and scheduled meetings may be used with the API. For example, to invite an attendee to the series, use the ID of the meeting series with the [Create a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/create-a-meeting-invitee) endpoint. Or, to invite someone to just one scheduled instance of a meeting, use the ID of the scheduled meeting instead.

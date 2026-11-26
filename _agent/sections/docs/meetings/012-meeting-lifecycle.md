---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Meeting Lifecycle
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

## Meeting Lifecycle

### Meeting Auto Delete

**Auto Delete Options**

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte8c404bd322b8380/5f89ff7a2f59ae27f3d617b5/Delete-from-My-Meetings-when-Completed.jpg" width="450">

There's a `Delete from My Meetings when completed` option in Webex page of classic view. It's invisible in Webex page of modern view and the default value is `unchecked`.

If the `Delete from My Meetings when completed` option is `unchecked` for a meeting, there will be a mandatory `Delete after 180 days` option for the meeting.

**Auto Delete Cases**

1. If the `Delete from My Meetings when completed` option is `checked` for a non-recurring meeting, the meeting will be deleted automatically after the scheduled end time.
2. If the `Delete from My Meetings when completed` option is `unchecked` for a non-recurring meeting, the meeting will be deleted automatically 180 days after the scheduled end time.
3. If the `Delete from My Meetings when completed` option is `checked` for a meeting series, the entire meeting series will be deleted automatically after the scheduled end time of the last scheduled meeting of the meeting series.
4. If the `Delete from My Meetings when completed` option is `unchecked` for a meeting series, the entire meeting will be deleted automatically 180 days after the scheduled end time of the last scheduled meeting of the meeting series.

### Meeting Series Lifecycle

![Meeting Lifecycle Meeting Series](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt66ac4d5d17270ee4/5f89ff7af9d3bf27fac3c6eb/Meeting-Lifecycle-Meeting-Series.jpg)

1. A meeting series is created.
2. A scheduled meeting of the meeting series is started, or someone has joined the meeting before the host and is waiting in lobby.
3. The ongoing scheduled meeting has ended, but it has not passed the scheduled end time of the last scheduled meeting of the meeting series, or the meeting has not yet been started and the participants which were previously waiting in lobby have left the meeting.
4. The ongoing scheduled meeting is ended, and it has passed the scheduled end time of the last scheduled meeting of the meeting series.
5. It has passed the scheduled end time of the last scheduled meeting of the meeting series.
6. The meeting series is deleted manually or automatically after it's been expired.
7. The meeting series is deleted manually.

### Scheduled Meeting Lifecycle

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt31af4933e75e9db3/5f89ff78ace59e4b8291844f/Meeting-Lifecycle-Scheduled-Meeting.jpg" width="520">

1. The parent meeting series is created. Any scheduled meeting other than the first one of the meeting series is `scheduled` and it can be started in the future.
2. The parent meeting series is created. The first scheduled meeting of the meeting series is `ready` and it can be started immediately.
3. It has passed the scheduled end time of the previous scheduled meeting. The subsequent scheduled meeting becomes `ready` and it can be started immediately.
4. The previous `ready` scheduled meeting has been started and ended, and it has passed its scheduled end time. This scheduled meeting becomes `ended`.
5. The previous `ready` scheduled meeting has never been started, and it has passed its scheduled end time. This scheduled meeting becomes `missed`.
6. The scheduled meeting is deleted manually or it's deleted when the parent meeting series is deleted maunally.
7. The scheduled meeting is deleted manually or it's deleted when the parent meeting series is deleted maunally or automatically.
8. The scheduled meeting is deleted manually or it's deleted when the parent meeting series is deleted maunally.
9. The scheduled meeting is deleted manually or it's deleted when the parent meeting series is deleted maunally or automatically.

### Meeting Lifecycle

![Meeting Lifecycle Meeting](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb1870666e295c7aa/5f89ff78271ecf4a1a6456c0/Meeting-Lifecycle-Meeting.jpg)

1. A locked meeting has been joined by participants, but no hosts have joined.
2. The meeting has been started and not ended yet.
3. The participants in lobby have been admitted to meeting.
4. The meeting has ended.

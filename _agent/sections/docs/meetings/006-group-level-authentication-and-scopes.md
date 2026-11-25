---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Group Level Authentication and Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Group Level Authentication and Scopes

A [service app](https://developer.webex.com/docs/service-apps) can be authorized with group level privileges including the groups and sites it manages. A service app with group level privileges can access or manage resources at group level.



| Scope | Usage | Accessible APIs |
|---|---|---|
| `meeting:group_meeting_read` | Access resources at group level | [List Group Recordings](https://developer.webex.com/docs/api/v1/recordings/list-group-recordings)<br/>[Get Group Recording Details](https://developer.webex.com/docs/api/v1/recordings/get-group-recording-details)<br/>[List Group Meetings](https://developer.webex.com/docs/api/v1/meetings/list-group-meetings) |
| `meeting:group_meeting_write` | Manage resources at group level | [Patch a Group Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-group-meeting)<br/>[Update Group Meeting Control Status](https://developer.webex.com/docs/api/v1/meetings/update-group-meeting-control-status) |

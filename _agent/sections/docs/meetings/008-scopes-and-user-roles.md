---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes and User Roles
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Scopes and User Roles

The table below lists the relationship between scopes and user roles:



| Scope | Role |
|---|---|
| `meeting:admin_schedule_read`<br/>`meeting:admin_schedule_write`<br/>`meeting:admin_recordings_read`<br/>`meeting:admin_recordings_write`<br/>`meeting:admin_transcripts_read`<br/>`meeting:admin_preferences_read`<br/>`meeting:admin_preferences_write`<br/>`meeting:admin_participants_read` | Full admin<br/>Content admin |
| `meeting:admin_config_read`<br/>`meeting:admin_config_write` | Site admin |
| `meeting:group_meeting_read`<br/>`meeting:group_meeting_write` | Group admin |
| `spark-compliance:meetings_read`<br/>`spark-compliance:meetings_write` | Compliance officer |
| `meeting:schedules_read`<br/>`meeting:schedules_write`<br/>`meeting:recordings_read`<br/>`meeting:recordings_write`<br/>`meeting:transcripts_read`<br/>`meeting:transcripts_write`<br/>`meeting:preferences_read`<br/>`meeting:preferences_write`<br/>`meeting:participants_read`<br/>`meeting:participants_write`<br/>`meeting:controls_read`<br/>`meeting:controls_write` | Individual user |
| `webex-squared:locus_participant`<br/>`spark:all` | Guest Issuer |

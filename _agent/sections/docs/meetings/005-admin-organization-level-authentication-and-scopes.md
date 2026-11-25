---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Admin/Organization Level Authentication and Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Admin/Organization Level Authentication and Scopes

Webex developers now have the ability to leverage admin level scopes in their integrations. These new scopes allow WebEx Admin grant scopes to integrations on behalf of other users. This allows developers and admins flexibility in creating integrations to meet their needs and can lessen the need for individual users of an integration to perform an OAuth grant.

Several conditions and restrictions apply to organizations that want to authorize an integration that utilizes these admin level scopes.

The `spark:all` scope is required for the [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API when `roomId` is specified.

* The admin that authorizes the integration for an organization (meeting:admin_* scopes) must be a full org admin. This admin must also be a site admin for the site or sites that contain the users they wish the integration to be able to act on behalf of.
* Partners: Partner admins who are also full org admins for their own org are not permitted to authorize integrations that use these admin level scopes for their customer's org. They are however able to authorize these types of integrations in their own org as per the previous requirement.

In support of this functionality the admin must grant the integration the following admin scopes:



| Scope | Usage | Accessible APIs |
|---|---|---|
| `meeting:admin_schedule_read` | Retrieve meetings of all WebEx users of your organization | [Get a Meeting](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting)<br/>[Get a Meeting By an Admin](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting-by-an-admin)<br/>[List Meetings](https://developer.webex.com/docs/api/v1/meetings/list-meetings)<br/>[List Meetings By an Admin](https://developer.webex.com/docs/api/v1/meetings/list-meetings-by-an-admin)<br/>[List Meetings of a Meeting Series](https://developer.webex.com/docs/api/v1/meetings/list-meetings-of-a-meeting-series)<br/>[List Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees/list-meeting-invitees)<br/>[Get a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/get-a-meeting-invitee)<br/>[Get registration form for a meeting](https://developer.webex.com/docs/api/v1/meetings/get-registration-form-for-a-meeting)<br/>[Get Detailed Information for a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/get-detailed-information-for-a-meeting-registrant)<br/>[List Meeting Registrants](https://developer.webex.com/docs/api/v1/meetings/list-meeting-registrants)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks) for Meetings |
| `meeting:admin_schedule_write` | Create, manage, or cancel meetings of all WebEx users of your organization | [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting)<br/>[Update a Meeting](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting)<br/>[Patch a Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-meeting)<br/>[Delete a Meeting](https://developer.webex.com/docs/api/v1/meetings/delete-a-meeting)<br/>[Create a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/create-a-meeting-invitee)<br/>[Update a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/update-a-meeting-invitee)<br/>[Delete a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/delete-a-meeting-invitee)<br/>[Reassign Meetings to a New Host](https://developer.webex.com/docs/api/v1/meetings/reassign-meetings-to-a-new-host) |
| `meeting:admin_recordings_read` | Retrieve recordings and meeting archive reports of all WebEx users of your organization | [Get Recording Details](https://developer.webex.com/docs/api/v1/recordings/get-recording-details)<br/>[List Recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings)<br/>[Query Recordings](https://developer.webex.com/docs/api/v1/recordings/query-recordings)<br/>[List Recordings For an Admin or Compliance Officer](https://developer.webex.com/docs/api/v1/recordings/list-recordings-for-an-admin-or-compliance-officer)<br/>[Query Recordings For an Admin or Compliance Officer](https://developer.webex.com/docs/api/v1/recordings/query-recordings-for-an-admin-or-compliance-officer)<br/>[List of Recording Audit Report Summaries](https://developer.webex.com/docs/api/v1/recording-report/list-of-recording-audit-report-summaries)<br/>[Get Recording Audit Report Details](https://developer.webex.com/docs/api/v1/recording-report/get-recording-audit-report-details)<br/>[List Meeting Archive Summaries](https://developer.webex.com/docs/api/v1/recording-report/list-meeting-archive-summaries)<br/>[Get Meeting Archive Details](https://developer.webex.com/docs/api/v1/recording-report/get-meeting-archive-details)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks) |
| `meeting:admin_recordings_write` | Manage or delete recordings of all WebEx users of your organization | [Delete a Recording](https://developer.webex.com/docs/api/v1/recordings/delete-a-recording)<br/>[Delete a Recording By an Admin](https://developer.webex.com/docs/api/v1/recordings/delete-a-recording-by-an-admin)<br/>[Move Recordings into the Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/move-recordings-into-the-recycle-bin)<br/>[Restore Recordings from Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/restore-recordings-from-recycle-bin)<br/>[Purge Recordings from Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/purge-recordings-from-recycle-bin)<br/>[Share a Recording](https://developer.webex.com/docs/api/v1/recordings/share-a-recording)<br/>[Share a Recording Link](https://developer.webex.com/docs/api/v1/recordings/share-a-recording-link) |
| `meeting:admin_transcripts_read` | Retrieve Webex meetings transcripts of all WebEx users of your organization | [List Meeting Transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-meeting-transcripts)<br/>[Download a meeting transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/download-a-meeting-transcript) |
| `meeting:admin_preferences_read` | Retrieve Webex meeting preferences of all WebEx users of your organization | [Get Meeting Preference Details](https://developer.webex.com/docs/api/v1/meeting-preferences/get-meeting-preference-details)<br/>[Get Personal Meeting Room Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-personal-meeting-room-options)<br/>[Get Audio Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-audio-options)<br/>[Get Video Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-video-options)<br/>[Get Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-scheduling-options)<br/>[Get Site List](https://developer.webex.com/docs/api/v1/meeting-preferences/get-site-list) |
| `meeting:admin_preferences_write` | Manage meeting preferences of all WebEx users of your organization | [Update Personal Meeting Room Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-personal-meeting-room-options)<br/>[Update Audio Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-audio-options)<br/>[Update Video Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-video-options)<br/>[Update Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-scheduling-options)<br/>[Update Default Site](https://developer.webex.com/docs/api/v1/meeting-preferences/update-default-site)<br/>[Batch Refresh Personal Meeting Room ID](https://developer.webex.com/docs/api/v1/meeting-preferences/batch-refresh-personal-meeting-room-id) |
| `meeting:admin_participants_read` | Read participant information from meetings for all WebEx users of your organization | [Get Meeting Participant Details](https://developer.webex.com/docs/api/v1/meeting-participants/get-meeting-participant-details)<br/>[List Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants/list-meeting-participants)<br/>[Query Meeting Participants with Email](https://developer.webex.com/docs/api/v1/meeting-participants/query-meeting-participants-with-email)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks) for Meeting Participants |
| `meeting:admin_config_read` | Retrieve Webex meeting configurations as an administrator | [List Meeting Usage Reports](https://developer.webex.com/docs/api/v1/meetings-summary-report/list-meeting-usage-reports)<br/>[List Meeting Attendee Reports](https://developer.webex.com/docs/api/v1/meetings-summary-report/list-meeting-attendee-reports) |
| `meeting:admin_config_write` | Manage Webex meeting configurations as an administrator | [Batch Refresh Personal Meeting Room ID](https://developer.webex.com/docs/api/v1/meeting-preferences/batch-refresh-personal-meeting-room-id) |

The admin feature applies to both CI-enabled or CI-linked Webex sites. The managed user account (host) does not need to be CI-enabled/CI-linked.

In support of this feature, the following will be allowed as query parameters on GET requests and as valid attributes in the request body of POST and PUT commands:

* `hostEmail` - When set as a query parameter on a GET request made by an admin, the response will be the meetings where the user of `hostEmail` is the meeting host or an invitee, not the meetings for the admin user. When set as part of the request body sent to a POST method by an admin, the specified user will be the host of the meeting if he belongs to a site managed by the admin user. When set as part of the request body sent to a PUT or PATCH method, the field is not editable and is only used to update or patch a meeting on behalf of the real meeting host. Please use the [Reassign Meetings to a New Host](https://developer.webex.com/docs/api/v1/meetings/reassign-meetings-to-a-new-host) API if you need to update the meeting host. The meeting will belong to the specified host's default site unless the `siteUrl` attribute is used to override this.
* `siteUrl` - optional - When set as a query parameter on a GET request, the response will be restricted to the meetings that belong to the specified site that are hosted by the caller of the API, or by the user specified via the `hostEmail` parameter. When set as part of the request body sent to a POST or PUT method, this attribute allows the caller of the API to create a meeting in a non-preferred site for a host whose account is associated with multiple sites.

Developers can become aware of the allowable values for `siteUrl` by querying the [GET /meetingPreferences/sites](https://developer.webex.com/docs/api/v1/meeting-preferences/get-site-list) API.

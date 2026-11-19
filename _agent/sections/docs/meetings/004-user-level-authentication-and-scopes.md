---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- User Level Authentication and Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## User Level Authentication and Scopes

Webex REST API authentication is described in detail in the [Integrations Guide](https://developer.webex.com/docs/integrations). The following scopes are required to use the meetings-related API resources:

The `spark:all` scope is required for the [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API when `roomId` is specified.



| Scope | Usage | Accessible APIs |
|---|---|---|
| `meeting:schedules_read` | Retrieve your Webex meeting lists and details | [List Meetings of a Meeting Series](https://developer.webex.com/docs/api/v1/meetings/list-meetings-of-a-meeting-series)<br/>[Get a Meeting](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting)<br/>[List Meetings](https://developer.webex.com/docs/api/v1/meetings/list-meetings)<br/>[Join a Meeting](https://developer.webex.com/docs/api/v1/meetings/join-a-meeting)<br/>[List Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees/list-meeting-invitees)<br/>[Get a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/get-a-meeting-invitee)<br/>[List Meeting Transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-meeting-transcripts)<br/>[Download a meeting transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/download-a-meeting-transcript)<br/>[Get registration form for a meeting](https://developer.webex.com/docs/api/v1/meetings/get-registration-form-for-a-meeting)<br/>[Get Detailed Information for a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/get-detailed-information-for-a-meeting-registrant)<br/>[List Meeting Registrants](https://developer.webex.com/docs/api/v1/meetings/list-meeting-registrants)<br/>[List Meeting Session Types](https://developer.webex.com/docs/api/v1/meetings/list-meeting-session-types)<br/>[Get a Meeting Session Type](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting-session-type)<br/>[List Meeting Attendee Reports](https://developer.webex.com/docs/api/v1/meetings-summary-report/list-meeting-attendee-reports)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks) for Meetings |
| `meeting:schedules_write` | Create, manage, or cancel your scheduled Webex meetings | [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting)<br/>[Update a Meeting](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting)<br/>[Patch a Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-meeting)<br/>[Delete a Meeting](https://developer.webex.com/docs/api/v1/meetings/delete-a-meeting)<br/>[Create a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/create-a-meeting-invitee)<br/>[Update a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/update-a-meeting-invitee)<br/>[Delete a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/delete-a-meeting-invitee)<br/>[Create Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees/create-meeting-invitees)<br/>[Batch Update Meeting Registrants status](https://developer.webex.com/docs/api/v1/meetings/batch-update-meeting-registrants-status)<br/>[Register a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/register-a-meeting-registrant) |
| `meeting:recordings_read` | Retrieve your Webex meeting recordings for playback and recording reports | [List Recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings)<br/>[Query Recordings](https://developer.webex.com/docs/api/v1/recordings/query-recordings)<br/>[Get Recording Details](https://developer.webex.com/docs/api/v1/recordings/get-recording-details)<br/>[List of Recording Audit Report Summaries](https://developer.webex.com/docs/api/v1/recording-report/list-of-recording-audit-report-summaries)<br/>[Get Recording Audit Report Details](https://developer.webex.com/docs/api/v1/recording-report/get-recording-audit-report-details)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks) |
| `meeting:recordings_write` | Manage or delete your meeting recordings for playback | [Delete a Recording](https://developer.webex.com/docs/api/v1/recordings/delete-a-recording)<br/>[Move Recordings into the Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/move-recordings-into-the-recycle-bin)<br/>[Restore Recordings from Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/restore-recordings-from-recycle-bin)<br/>[Purge Recordings from Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/purge-recordings-from-recycle-bin)<br/>[Share a Recording](https://developer.webex.com/docs/api/v1/recordings/share-a-recording)<br/>[Share a Recording Link](https://developer.webex.com/docs/api/v1/recordings/share-a-recording-link) |
| `meeting:transcripts_read` | Retrieve your Webex meetings transcripts | [List Meeting Transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-meeting-transcripts)<br/>[Download a meeting transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/download-a-meeting-transcript)<br/>[List Snippets of a Meeting Transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-snippets-of-a-meeting-transcript)<br/>[Get a Transcript Snippet](https://developer.webex.com/docs/api/v1/meeting-transcripts/get-a-transcript-snippet) |
| `meeting:transcripts_write` | Manage your Webex meeting transcript snippets | [Update a Transcript Snippet](https://developer.webex.com/docs/api/v1/meeting-transcripts/update-a-transcript-snippet) |
| `meeting:summaries_read` | Retrieve your Webex meetings summaries | [Get Summary by Meeting ID](https://developer.webex.com/docs/api/v1/meeting-summaries/get-summary-by-meeting-id) |
| `meeting:summaries_write` | Manage your Webex meeting summaries | [Delete a Summary](https://developer.webex.com/docs/api/v1/meeting-summaries/delete-a-summary) |
| `meeting:preferences_read` | Retrieve your Webex meeting preferences | [Get Meeting Preference Details](https://developer.webex.com/docs/api/v1/meeting-preferences/get-meeting-preference-details)<br/>[Get Personal Meeting Room Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-personal-meeting-room-options)<br/>[Get Audio Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-audio-options)<br/>[Get Video Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-video-options)<br/>[Get Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-scheduling-options)<br/>[Get Site List](https://developer.webex.com/docs/api/v1/meeting-preferences/get-site-list) |
| `meeting:preferences_write` | Edit your Webex meeting preferences | [Update Personal Meeting Room Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-personal-meeting-room-options)<br/>[Update Audio Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-audio-options)<br/>[Update Video Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-video-options)<br/>[Update Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-scheduling-options)<br/>[Update Default Site](https://developer.webex.com/docs/api/v1/meeting-preferences/update-default-site) |
| `meeting:participants_read` | Read participant information from meetings | [List Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants/list-meeting-participants)<br/>[Get Meeting Participant Details](https://developer.webex.com/docs/api/v1/meeting-participants/get-meeting-participant-details)<br/>[Query Meeting Participants with Email](https://developer.webex.com/docs/api/v1/meeting-participants/query-meeting-participants-with-email)<br/>[List Meeting Attendee Reports](https://developer.webex.com/docs/api/v1/meetings-summary-report/list-meeting-attendee-reports)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks) for Meeting Participants |
| `meeting:participants_write` | Manage participants within meetings | [Update a Participant](https://developer.webex.com/docs/api/v1/meeting-participants/update-a-participant)<br/>[Admit Participants](https://developer.webex.com/docs/api/v1/meeting-participants/admit-participants)<br/>[Call Out a SIP Participant](https://developer.webex.com/docs/api/v1/meeting-participants/call-out-a-sip-participant)<br/>[Cancel Calling Out a SIP Participant](https://developer.webex.com/docs/api/v1/meeting-participants/cancel-calling-out-a-sip-participant) |
| `meeting:controls_read` | Read meeting control information for in-progress meetings | [Get Meeting Control Status](https://developer.webex.com/docs/api/v1/meetings/get-meeting-control-status) |
| `meeting:controls_write` | Update meeting controls for in-progress meetings | [Update Meeting Control Status](https://developer.webex.com/docs/api/v1/meetings/update-meeting-control-status) |



> **Info**
>
> Remember, when choosing scopes for your app, only select the scopes your application will need.

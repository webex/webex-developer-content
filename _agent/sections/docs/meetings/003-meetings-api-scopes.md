---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings API Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Meetings API Scopes

The table below lists all meetings APIs and their required scopes at different levels.

The `spark:all` scope is required for the [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API when `roomId` is specified.



| Resource | API | User Level Scopes | Admin/Org Level Scopes | [Compliance Officer](https://developer.webex.com/docs/compliance#compliance) Level Scopes | Group Level Scopes                                              |
|---|---|---|---|---|-----------------------------------------------------------------|
| Meetings | [List Meetings of a Meeting Series](https://developer.webex.com/docs/api/v1/meetings/list-meetings-of-a-meeting-series) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A                                                             |
|  | [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Get a Meeting](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Get a Meeting By an Admin](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting-by-an-admin) | N/A | `meeting:admin_schedule_read` | `spark-compliance:meetings_read` | N/A |
|  | [List Meetings](https://developer.webex.com/docs/api/v1/meetings/list-meetings) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [List Meetings By an Admin](https://developer.webex.com/docs/api/v1/meetings/list-meetings-by-an-admin) | N/A | `meeting:admin_schedule_read` | `spark-compliance:meetings_read` | N/A |
|  | [List Group Meetings](https://developer.webex.com/docs/api/v1/meetings/list-group-meetings) | N/A | N/A | N/A | `meeting:group_meeting_read` |
|  | [Patch a Group Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-group-meeting) | N/A | N/A | N/A | `meeting:group_meeting_write` |
|  | [Update Group Meeting Control Status](https://developer.webex.com/docs/api/v1/meetings/update-group-meeting-control-status) | N/A | N/A | N/A | `meeting:group_meeting_write` |
|  | [Update a Meeting](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Patch a Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-meeting) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Delete a Meeting](https://developer.webex.com/docs/api/v1/meetings/delete-a-meeting) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Join a Meeting](https://developer.webex.com/docs/api/v1/meetings/join-a-meeting) | `meeting:schedules_read` | N/A | N/A | N/A |
|  | [Get Meeting Control Status](https://developer.webex.com/docs/api/v1/meetings/get-meeting-control-status) | `meeting:controls_read` | N/A | N/A | N/A |
|  | [Update Meeting Control Status](https://developer.webex.com/docs/api/v1/meetings/update-meeting-control-status) | `meeting:controls_write` | N/A | N/A | N/A |
|  | [Get registration form for a meeting](https://developer.webex.com/docs/api/v1/meetings/get-registration-form-for-a-meeting) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Get Detailed Information for a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/get-detailed-information-for-a-meeting-registrant) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [List Meeting Registrants](https://developer.webex.com/docs/api/v1/meetings/list-meeting-registrants) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Batch Update Meeting Registrants status](https://developer.webex.com/docs/api/v1/meetings/batch-update-meeting-registrants-status) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Register a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/register-a-meeting-registrant) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [List Meeting Session Types](https://developer.webex.com/docs/api/v1/meetings/list-meeting-session-types) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Get a Meeting Session Type](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting-session-type) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Reassign Meetings to a New Host](https://developer.webex.com/docs/api/v1/meetings/reassign-meetings-to-a-new-host) | N/A | `meeting:admin_schedule_write` | N/A | N/A |
| Meeting Invitees | [List Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees/list-meeting-invitees) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Create a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/create-a-meeting-invitee) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Create Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees/create-meeting-invitees) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Get a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/get-a-meeting-invitee) | `meeting:schedules_read` | `meeting:admin_schedule_read` | N/A | N/A |
|  | [Update a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/update-a-meeting-invitee) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
|  | [Delete a Meeting Invitee](https://developer.webex.com/docs/api/v1/meeting-invitees/delete-a-meeting-invitee) | `meeting:schedules_write` | `meeting:admin_schedule_write` | N/A | N/A |
| Meeting Participants | [List Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants/list-meeting-participants) | `meeting:participants_read` | `meeting:admin_participants_read` | `spark-compliance:meetings_read` | N/A |
|  | [Get Meeting Participant Details](https://developer.webex.com/docs/api/v1/meeting-participants/get-meeting-participant-details) | `meeting:participants_read` | `meeting:admin_participants_read` | `spark-compliance:meetings_read` | N/A |
|  | [Query Meeting Participants with Email](https://developer.webex.com/docs/api/v1/meeting-participants/query-meeting-participants-with-email) | `meeting:participants_read` | `meeting:admin_participants_read` | `spark-compliance:meetings_read` | N/A |
|  | [Update a Participant](https://developer.webex.com/docs/api/v1/meeting-participants/update-a-participant) | `meeting:participants_write` | N/A | N/A | N/A |
|  | [Admit Participants](https://developer.webex.com/docs/api/v1/meeting-participants/admit-participants) | `meeting:participants_write` | N/A | N/A | N/A |
|  | [Call Out a SIP Participant](https://developer.webex.com/docs/api/v1/meeting-participants/call-out-a-sip-participant) | `meeting:participants_write` | N/A | N/A | N/A |
|  | [Cancel Calling Out a SIP Participant](https://developer.webex.com/docs/api/v1/meeting-participants/cancel-calling-out-a-sip-participant) | `meeting:participants_write` | N/A | N/A | N/A |
| Recordings | [List Recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings) | `meeting:recordings_read` | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [Query Recordings](https://developer.webex.com/docs/api/v1/recordings/query-recordings) | `meeting:recordings_read` | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [List Recordings For an Admin or Compliance Officer](https://developer.webex.com/docs/api/v1/recordings/list-recordings-for-an-admin-or-compliance-officer) | N/A | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [Query Recordings For an Admin or Compliance Officer](https://developer.webex.com/docs/api/v1/recordings/query-recordings-for-an-admin-or-compliance-officer) | N/A | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [Get Recording Details](https://developer.webex.com/docs/api/v1/recordings/get-recording-details) | `meeting:recordings_read` | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [Delete a Recording](https://developer.webex.com/docs/api/v1/recordings/delete-a-recording) | `meeting:recordings_write` | `meeting:admin_recordings_write` | `spark-compliance:meetings_write` | N/A |
|  | [Delete a Recording By an Admin](https://developer.webex.com/docs/api/v1/recordings/delete-a-recording-by-an-admin) | N/A | `meeting:admin_recordings_write` | N/A | N/A |
|  | [Move Recordings into the Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/move-recordings-into-the-recycle-bin) | `meeting:recordings_write` | `meeting:admin_recordings_write` | N/A | N/A |
|  | [Restore Recordings from Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/restore-recordings-from-recycle-bin) | `meeting:recordings_write` | `meeting:admin_recordings_write` | N/A | N/A |
|  | [Purge Recordings from Recycle Bin](https://developer.webex.com/docs/api/v1/recordings/purge-recordings-from-recycle-bin) | `meeting:recordings_write` | `meeting:admin_recordings_write` | N/A | N/A |
|  | [Share a Recording](https://developer.webex.com/docs/api/v1/recordings/share-a-recording) | `meeting:recordings_write` | `meeting:admin_recordings_write` | N/A | N/A |
|  | [Share a Recording Link](https://developer.webex.com/docs/api/v1/recordings/share-a-recording-link) | `meeting:recordings_write` | `meeting:admin_recordings_write` | N/A | N/A |
|  | [List Group Recordings](https://developer.webex.com/docs/api/v1/recordings/list-group-recordings) | N/A | N/A | N/A | `meeting:group_meeting_read` |
|  | [Get Group Recording Details](https://developer.webex.com/docs/api/v1/recordings/get-group-recording-details) | N/A | N/A | N/A | `meeting:group_meeting_read` |
| Recording Reports | [List of Recording Audit Report Summaries](https://developer.webex.com/docs/api/v1/recording-report/list-of-recording-audit-report-summaries) | `meeting:recordings_read` | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [Get Recording Audit Report Details](https://developer.webex.com/docs/api/v1/recording-report/get-recording-audit-report-details) | `meeting:recordings_read` | `meeting:admin_recordings_read` | `spark-compliance:meetings_read` | N/A |
|  | [List Meeting Archive Summaries](https://developer.webex.com/docs/api/v1/recording-report/list-meeting-archive-summaries) | N/A | `meeting:admin_recordings_read` | N/A | N/A |
|  | [Get Meeting Archive Details](https://developer.webex.com/docs/api/v1/recording-report/get-meeting-archive-details) | N/A | `meeting:admin_recordings_read` | N/A | N/A |
| Meeting Transcripts | [List Meeting Transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-meeting-transcripts) | `meeting:transcripts_read`<br/>`meeting:schedules_read` | `meeting:admin_transcripts_read` | `spark-compliance:meetings_read` | N/A |
|  | [Download a meeting transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/download-a-meeting-transcript) | `meeting:transcripts_read`<br/>`meeting:schedules_read` | `meeting:admin_transcripts_read` | `spark-compliance:meetings_read` | N/A |
|  | [List Snippets of a Meeting Transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-snippets-of-a-meeting-transcript) | `meeting:transcripts_read` | N/A | `spark-compliance:meetings_read` | N/A |
|  | [Get a Transcript Snippet](https://developer.webex.com/docs/api/v1/meeting-transcripts/get-a-transcript-snippet) | `meeting:transcripts_read` | N/A | `spark-compliance:meetings_read` | N/A |
|  | [Update a Transcript Snippet](https://developer.webex.com/docs/api/v1/meeting-transcripts/update-a-transcript-snippet) | `meeting:transcripts_write` | N/A | `spark-compliance:meetings_write` | N/A |
| Meeting Summaries | [Get Summary by Meeting ID](https://developer.webex.com/docs/api/v1/meeting-summaries/get-summary-by-meeting-id) | `meeting:summaries_read` | N/A | `spark-compliance:meetings_read` | N/A |
|  | [Delete a Summary](https://developer.webex.com/docs/api/v1/meeting-summaries/delete-a-summary) | `meeting:summaries_write` | N/A | `spark-compliance:meetings_write` | N/A |
| Meeting Preferences | [Get Meeting Preference Details](https://developer.webex.com/docs/api/v1/meeting-preferences/get-meeting-preference-details) | `meeting:preferences_read` | `meeting:admin_preferences_read` | N/A | N/A |
|  | [Get Personal Meeting Room Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-personal-meeting-room-options) | `meeting:preferences_read` | `meeting:admin_preferences_read` | N/A | N/A |
|  | [Update Personal Meeting Room Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-personal-meeting-room-options) | `meeting:preferences_write` | `meeting:admin_preferences_write` | N/A | N/A |
|  | [Get Audio Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-audio-options) | `meeting:preferences_read` | `meeting:admin_preferences_read` | N/A | N/A |
|  | [Update Audio Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-audio-options) | `meeting:preferences_write` | `meeting:admin_preferences_write` | N/A | N/A |
|  | [Get Video Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-video-options) | `meeting:preferences_read` | `meeting:admin_preferences_read` | N/A | N/A |
|  | [Update Video Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-video-options) | `meeting:preferences_write` | `meeting:admin_preferences_write` | N/A | N/A |
|  | [Get Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/get-scheduling-options) | `meeting:preferences_read` | `meeting:admin_preferences_read` | N/A | N/A |
|  | [Update Scheduling Options](https://developer.webex.com/docs/api/v1/meeting-preferences/update-scheduling-options) | `meeting:preferences_write` | `meeting:admin_preferences_write` | N/A | N/A |
|  | [Get Site List](https://developer.webex.com/docs/api/v1/meeting-preferences/get-site-list) | `meeting:preferences_read` | `meeting:admin_preferences_read` | N/A | N/A |
|  | [Update Default Site](https://developer.webex.com/docs/api/v1/meeting-preferences/update-default-site) | `meeting:preferences_write` | `meeting:admin_preferences_write` | N/A | N/A |
|  | [Batch Refresh Personal Meeting Room ID](https://developer.webex.com/docs/api/v1/meeting-preferences/batch-refresh-personal-meeting-room-id) |  N/A  | `meeting:admin_preferences_write`<br/>`meeting:admin_config_write` | N/A | N/A |
| Meeting Reports | [List Meeting Usage Reports](https://developer.webex.com/docs/api/v1/meetings-summary-report/list-meeting-usage-reports) | N/A | `meeting:admin_config_read` | N/A | N/A |
|  | [List Meeting Attendee Reports](https://developer.webex.com/docs/api/v1/meetings-summary-report/list-meeting-attendee-reports) | `meeting:participants_read`<br/>`meeting:schedules_read` | `meeting:admin_config_read` | N/A | N/A |

Guest users can interact with regular Webex users via tokens generated by a [Guest Issuer](https://developer.webex.com/docs/guest-issuer) application. The table below lists the meetings APIs for guest issuer and the required scopes.

| Resource | API | [Guest Issuer](https://developer.webex.com/docs/guest-issuer) Scopes |
|---|---|---|
| Meetings | [Get Detailed Information for a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/get-detailed-information-for-a-meeting-registrant) | `webex-squared:locus_participant`<br/>`spark:all` |
|  | [List Meeting Registrants](https://developer.webex.com/docs/api/v1/meetings/list-meeting-registrants) | `webex-squared:locus_participant`<br/>`spark:all` |
|  | [Batch Update Meeting Registrants status](https://developer.webex.com/docs/api/v1/meetings/batch-update-meeting-registrants-status) | `webex-squared:locus_participant`<br/>`spark:all` |
|  | [Register a Meeting Registrant](https://developer.webex.com/docs/api/v1/meetings/register-a-meeting-registrant) | `webex-squared:locus_participant`<br/>`spark:all` |
|  | [Join a Meeting](https://developer.webex.com/docs/api/v1/meetings/join-a-meeting) | `webex-squared:locus_participant` |

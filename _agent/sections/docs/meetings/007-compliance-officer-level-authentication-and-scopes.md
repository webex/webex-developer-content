---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Compliance Officer Level Authentication and Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Compliance Officer Level Authentication and Scopes

An administrator user can be associated with a specific role to become a [Compliance Officer](https://developer.webex.com/docs/compliance#compliance). The role of a compliance officer is to ensure that a company is conducting its business in full compliance with all laws and regulations that pertain to its particular industry, as well as professional standards, accepted business practices, and internal standards. The following scopes are required to use the meetings-related API resources as a Compliance Officer:



| Scope | Usage | Accessible APIs |
|---|---|---|
| `spark-compliance:meetings_read` | Access to read recordings, transcripts, chats, meeting participants, meeting closed captions, and meeting Q and A resources in your user’s organization | [Get Recording Details](https://developer.webex.com/docs/api/v1/recordings/get-recording-details)<br/>[List Recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings)<br/>[Query Recordings](https://developer.webex.com/docs/api/v1/recordings/query-recordings)<br/>[List Recordings For an Admin or Compliance Officer](https://developer.webex.com/docs/api/v1/recordings/list-recordings-for-an-admin-or-compliance-officer)<br/>[Query Recordings For an Admin or Compliance Officer](https://developer.webex.com/docs/api/v1/recordings/query-recordings-for-an-admin-or-compliance-officer)<br/>[Get Meeting Participant Details](https://developer.webex.com/docs/api/v1/meeting-participants/get-meeting-participant-details)<br/>[List Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants/list-meeting-participants)<br/>[Query Meeting Participants with Email](https://developer.webex.com/docs/api/v1/meeting-participants/query-meeting-participants-with-email)<br/>[List Meeting Transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-meeting-transcripts)<br/>[List Meeting Transcripts For Compliance Officer](https://developer.webex.com/api/v1/meeting-transcripts/list-meeting-transcripts-for-compliance-officer)<br/>[Download a meeting transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/download-a-meeting-transcript)<br/>[List Snippets of a Meeting Transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/list-snippets-of-a-meeting-transcript)<br/>[Get a Transcript Snippet](https://developer.webex.com/docs/api/v1/meeting-transcripts/get-a-transcript-snippet)<br/>[List of Recording Audit Report Summaries](https://developer.webex.com/docs/api/v1/recording-report/list-of-recording-audit-report-summaries)<br/>[Get Recording Audit Report Details](https://developer.webex.com/docs/api/v1/recording-report/get-recording-audit-report-details)<br/>[Webhook APIs](https://developer.webex.com/docs/api/v1/webhooks)<br/>[List Meeting Polls](https://developer.webex.com/docs/api/v1/meeting-polls/list-meeting-polls)<br/>[Get Meeting PollResults](https://developer.webex.com/docs/api/v1/meeting-polls/get-meeting-pollresults)<br/>[List Respondents of a Question](https://developer.webex.com/docs/api/v1/meeting-polls/list-respondents-of-a-question)<br/>[List Meeting Chats](https://developer.webex.com/docs/api/v1/meeting-chats/list-meeting-chats)<br/>[List Meeting Closed Captions](https://developer.webex.com/docs/api/v1/meeting-closed-captions/list-meeting-closed-captions)<br/>[List Meeting Closed Caption Snippets](https://developer.webex.com/docs/api/v1/meeting-closed-captions/list-meeting-closed-caption-snippets)<br/>[Download Meeting Closed Caption Snippets](https://developer.webex.com/docs/api/v1/meeting-closed-captions/download-meeting-closed-caption-snippets)<br/>[List Meeting Q and A](https://developer.webex.com/docs/api/v1/meeting-q-and-a/list-meeting-q-and-a)<br/>[List Answers of a Question](https://developer.webex.com/docs/api/v1/meeting-q-and-a/list-answers-of-a-question)<br/>[Get a Meeting By an Admin](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting-by-an-admin)<br/>[List Meetings By an Admin](https://developer.webex.com/docs/api/v1/meetings/list-meetings-by-an-admin)<br/>[Get Summary For Compliance Officer](https://developer.webex.com/docs/api/v1/meeting-summaries/get-summary-for-compliance-officer) |
| `spark-compliance:meetings_write` | Access to delete recordings, transcripts, chats, and update transcripts resources in your user’s organization | [Delete a Recording](https://developer.webex.com/docs/api/v1/recordings/delete-a-recording)<br/>[Update a Transcript Snippet](https://developer.webex.com/docs/api/v1/meeting-transcripts/update-a-transcript-snippet)<br/>[Delete a Transcript](https://developer.webex.com/docs/api/v1/meeting-transcripts/delete-a-transcript)<br/>[Delete Meeting Chats](https://developer.webex.com/docs/api/v1/meeting-chats/delete-meeting-chats)<br/>[Delete Meeting Summaries](https://developer.webex.com/docs/api/v1/meeting-summaries/delete-a-summary) |

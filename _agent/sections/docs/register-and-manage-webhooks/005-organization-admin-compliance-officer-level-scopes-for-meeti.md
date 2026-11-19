---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [User Level Scopes for Meeting Related Webhooks](004-user-level-scopes-for-meeting-related-webhooks.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks

The following scopes are required to create, get, list, update or delete webhooks at organization level for meeting related resources:



| Scope                          | Resource                      | Usage                                                                                         |
|---------------------------------|--------------------------------|-----------------------------------------------------------------------------------------------|
| `meeting:admin_schedule_read`     | `meetings`                       | Manipulate webhooks of `meetings` resource as an admin                                        |
| `meeting:admin_participants_read` | `meetingParticipants`            | Manipulate webhooks of `meetingParticipants` resource as an admin                             |
| `meeting:admin_recordings_read`   | `recordings`                     | Manipulate webhooks of `recordings` resource as an admin                                      |
| `meeting:admin_transcripts_read`  | `meetingTranscripts`             | Manipulate webhooks of `meetingTranscripts` resource as an admin                              |
| `spark-compliance:meetings_read`  | `recordings, meetingTranscripts` | Manipulate webhooks of `recordings` and `meetingTranscripts` resource as a compliance officer |

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/register-and-manage-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- User Level Scopes for Meeting Related Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/register-and-manage-webhooks). [Full Markdown](../../../../docs/register-and-manage-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [Organization/Admin/Compliance Officer Level Scopes for Meeting Related Webhooks](005-organization-admin-compliance-officer-level-scopes-for-meeti.md)

## Article introduction

Register Webex Webhooks API notifications for Messaging, Meetings, Calling, and platform events, then manage registrations owned by your application.

## Selected section

## User Level Scopes for Meeting Related Webhooks

The following scopes are required to create, get, list, update or delete webhooks at user level for meeting related resources:



| Scope                    | Resource         | Usage                                                                  |
|---------------------------|---------------------|------------------------------------------------------------------------|
| `meeting:schedules_read`    | `meetings`            | Manipulate webhooks of `meetings` resource as a normal user            |
| `meeting:participants_read` | `meetingParticipants` | Manipulate webhooks of `meetingParticipants` resource as a normal user |
| `meeting:recordings_read`   | `recordings`          | Manipulate webhooks of `recordings` resource as a normal user          |
| `meeting:transcripts_read`  | `meetingTranscripts`  | Manipulate webhooks of `meetingTranscripts` resource as a normal user  |

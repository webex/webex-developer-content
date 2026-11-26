---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhook-event-reference
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhook-event-reference). [Full Markdown](../../../../docs/webhook-event-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Webhooks API resources, events, triggers, filters, and links to product-specific payload definitions.

## Selected section

## Meetings

| Resource | Event | Trigger | Supported filters |
| --- | --- | --- | --- |
| `meetings` | `created` | A new meeting was created. | `id` — Meeting Id.<br />`meetingNumber` — Meeting number.<br />`meetingType` — Meeting type.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetings` | `updated` | A meeting that you're in was updated. | `id` — Meeting Id.<br />`meetingNumber` — Meeting number.<br />`meetingType` — Meeting type.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetings` | `deleted` | A meeting that you're in was deleted. | `id` — Meeting Id.<br />`meetingNumber` — Meeting number.<br />`meetingType` — Meeting type.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetings` | `started` | A meeting was started. | `id` — Meeting Id.<br />`meetingNumber` — Meeting number.<br />`meetingType` — Meeting type.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetings` | `ended` | A meeting was ended. | `id` — Meeting Id.<br />`meetingNumber` — Meeting number.<br />`meetingType` — Meeting type.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `recordings` | `created` | A new recording was created. | `id` — Recording Id.<br />`meetingId` — Unique identifier for the parent meeting series, scheduled meeting or meeting instance for which recordings are being requested.<br />`scheduledMeetingId` — Unique identifier for the parent scheduled meeting which the recording belongs to.<br />`meetingSeriesId` — Unique identifier for the parent meeting series which the recording belongs to.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `recordings` | `updated` | A recording that you're in was updated. | `id` — Recording Id.<br />`meetingId` — Unique identifier for the parent meeting series, scheduled meeting or meeting instance for which recordings are being requested.<br />`scheduledMeetingId` — Unique identifier for the parent scheduled meeting which the recording belongs to.<br />`meetingSeriesId` — Unique identifier for the parent meeting series which the recording belongs to.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `recordings` | `deleted` | A recording that you're in was deleted permanently. There is no notification provided for moving a recording to the trash bin currently. | `id` — Recording Id.<br />`meetingId` — Unique identifier for the parent meeting series, scheduled meeting or meeting instance for which recordings are being requested.<br />`scheduledMeetingId` — Unique identifier for the parent scheduled meeting which the recording belongs to.<br />`meetingSeriesId` — Unique identifier for the parent meeting series which the recording belongs to.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetingParticipants` | `joined` | A participant has joined the meeting. | `id` — Participant Id.<br />`meetingId` — Meeting Instance Id.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostPersonId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetingParticipants` | `left` | A participant has left the meeting. | `id` — Participant Id.<br />`meetingId` — Meeting Instance Id.<br />`state` — Meeting state.<br />`hostEmail` — Email address for the meeting host.<br />`hostPersonId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |
| `meetingTranscripts` | `created` | A new transcript was created. | `id` — Transcript Id.<br />`meetingId` — Unique identifier for the parent meeting series, scheduled meeting or meeting instance for which transcripts are being requested.<br />`scheduledMeetingId` — Unique identifier for the parent scheduled meeting which the transcript belongs to.<br />`meetingSeriesId` — Unique identifier for the parent meeting series which the transcript belongs to.<br />`hostEmail` — Email address for the meeting host.<br />`hostUserId` — Unique identifier for meeting host.<br />`siteUrl` — Webex site URL to query. |

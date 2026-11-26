---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhook-event-reference
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Calling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhook-event-reference). [Full Markdown](../../../../docs/webhook-event-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Webhooks API resources, events, triggers, filters, and links to product-specific payload definitions.

## Selected section

## Calling

`telephony_calls`, `telephony_conference`, and `telephony_mwi` notifications are delivered only for Webex Calling users.

Check [interest registrations](https://developer.webex.com/docs/call-control#interest-registration) before expecting delivery. Detailed [Calling payload schemas](https://developer.webex.com/docs/call-control#webhook-payload-schemas) remain in the Calling guide. Converged recordings in the current catalog describe call recordings.

| Resource | Event | Trigger | Supported filters |
| --- | --- | --- | --- |
| `telephony_calls` | `created` | You started (originated) or received a call. | `personality` — limit to a particular call personality (`clickToDial`, `originator`, or `terminator`).<br />`state` — limit to a particular call state (`alerting`, `connected`, `connecting`, `disconnected`, `held`, or `remoteHeld`).<br />`number` — limit to calls to a particular address or number.<br />`personId` — limit to a particular person, by ID.<br />`callType` — limit to a particular call type (`emergency`, `external`, `location`, `organization`, `other`, or `repair`). |
| `telephony_calls` | `updated` | A call you started or received, was updated (e.g. call was answered, forwarded, resumed, etc.). | `personality` — limit to a particular call personality (`clickToDial`, `originator`, or `terminator`).<br />`state` — limit to a particular call state (`alerting`, `connected`, `connecting`, `disconnected`, `held`, or `remoteHeld`).<br />`number` — limit to calls to a particular address or number.<br />`personId` — limit to a particular person, by ID.<br />`callType` — limit to a particular call type (`emergency`, `external`, `location`, `organization`, `other`, or `repair`). |
| `telephony_calls` | `deleted` | A call you started or received, was disconnected (deleted). | `personality` — limit to a particular call personality (`clickToDial`, `originator`, or `terminator`).<br />`state` — limit to a particular call state (`alerting`, `connected`, `connecting`, `disconnected`, `held`, or `remoteHeld`).<br />`number` — limit to calls to a particular address or number.<br />`personId` — limit to a particular person, by ID.<br />`callType` — limit to a particular call type (`emergency`, `external`, `location`, `organization`, `other`, or `repair`). |
| `telephony_conference` | `created` | A conference is created. | |
| `telephony_conference` | `updated` | A conference is updated through other conference APIs (held, resumed, muted, unmuted, participantMuted, participantUnmuted, updated, participantDeafened, participantUndeafened). | |
| `telephony_conference` | `deleted` | A conference is deleted when the conference ends. | |
| `telephony_mwi` | `updated` | Your Webex Calling voicemail messages were updated (e.g. message was received, deleted, marked as read, or marked as unread). | |
| `telephony_agent` | `updated` | A call queue agent's state changed, the agent joined or left a queue, or the agent entered a wrap-up code. | `actorId` — limit to a particular actor, by ID.<br />`actorType` — limit to a particular actor type (`PEOPLE`, `PLACE`, or `VIRTUAL_LINE`). |
| `telephony_agentMonitoring` | `updated` | An agent monitoring status was updated when a queue call to an agent ends or is transferred. | `actorId` — limit to a particular actor, by ID.<br />`actorType` — limit to a particular actor type (`PEOPLE`, `PLACE`, or `VIRTUAL_LINE`). |
| `telephony_queue` | `updated` | A call queue event occurred (e.g. call added, answered, abandoned, bounced, overflowed, stranded, transferred, or policy applied). | `actorId` — limit to a particular actor, by ID. |
| `telephony_queueMonitoring` | `updated` | Real-time call center monitoring status was updated, including queue metrics and agent availability. | `actorId` — limit to a particular actor, by ID. |
| `convergedRecordings` | `created` | A new converged recording (for now call recording) was created. | `recordingId` — Recording ID.<br />`ownerId` — Identifier for the recording owner for which recordings are being requested.<br />`ownerEmail` — Email address for the recording owner.<br />`ownerType` — The owner type for the recording.<br />`storageRegion` — Unique identifier for the region where the recording is stored.<br />`serviceType` — Unique identifier for the service type which the recording belongs to.<br />`locationId` — Unique identifier for location. |
| `convergedRecordings` | `deleted` | A new converged recording (for now call recording) was deleted. | `recordingId` — Recording ID.<br />`ownerId` — Identifier for the recording owner for which recordings are being requested.<br />`ownerEmail` — Email address for the recording owner.<br />`ownerType` — The owner type for the recording.<br />`storageRegion` — Unique identifier for the region where the recording is stored.<br />`serviceType` — Unique identifier for the service type which the recording belongs to.<br />`locationId` — Unique identifier for location. |
| `convergedRecordings` | `updated` | A converged recording (for now call recording) was updated. | `recordingId` — Recording ID.<br />`ownerId` — Identifier for the recording owner for which recordings are being requested.<br />`ownerEmail` — Email address for the recording owner.<br />`ownerType` — The owner type for the recording.<br />`storageRegion` — Unique identifier for the region where the recording is stored.<br />`serviceType` — Unique identifier for the service type which the recording belongs to.<br />`locationId` — Unique identifier for location. |
| `uc_counters` | `updated` | A dedicated instance performance counter was updated. This is an organization-wide webhook for admins. The scope required to register this webhook is `wxc-dedicateduc:admin_perfmon_read`. | `clusterName` — The cluster name.<br />`hostName` — The host name.<br />`nodeType` — The node type.<br />`agentId` — The agent id. |

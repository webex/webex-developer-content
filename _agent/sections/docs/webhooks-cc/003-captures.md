---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Captures
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks-cc). [Full Markdown](../../../../docs/webhooks-cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Contact Center webhook event types, resource versions, and event-specific payload fields.

---

<a id="using-webhooks"></a>

<a id="overview"></a>

## Selected section

## Captures

The Capture resource is a snippet of media. Specifically, Captures are the recorded pieces of media produced from a Task. Supported channels are Voice, Chat, Email & Social (as applicable for the solution). There can be one or many Captures for any given Task. Captures are accessible for both open (voice only) and closed Tasks (all channels). Requires one of the following scopes cjp:config_read, cjp-analyzer:read.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `capture` | [`capture:available`](https://developer.webex.com/docs/webhooks-cc#capture-available) | The recording for a call is available after the call has ended. | `capture:1.0.0` |
| `recording` | [`recording:available`](https://developer.webex.com/docs/webhooks-cc#recording-available) | A recording is available for an interaction. | `recording:1.0.0` |
| `transcription` | [`transcription:available`](https://developer.webex.com/docs/webhooks-cc#transcription-available) | A transcript is available for an interaction. | `transcription:1.0.0` |

The existing `capture:available` webhook remains backward-compatible and continues to indicate recording availability. In addition, explicit `recording:available` and `transcription:available` webhook events are available for integrations that want separate recording and transcript readiness signals.

Use these events as follows:

- Subscribe to `capture:available` if your integration already relies on the existing recording-ready webhook behavior.
- Subscribe to `recording:available` if you want an explicit recording-ready signal while preserving the same general payload shape as `capture:available`.
- Subscribe to `transcription:available` if you want an explicit transcript-ready signal.
- Subscribe to more than one of these events if your integration needs both recording and transcript readiness.

When the beta additive events are enabled for your organization for voice interactions:

- `capture:available` and `recording:available` are both delivered for recording readiness
- the two events fan out from the same internal recording-available signal and therefore share the same event `id`
- `capture:available` keeps the existing payload shape
- `recording:available` adds the `contactType` and `channelType` fields

For transcript availability, integrations should use `transcription:available` for both voice and digital interactions. Its payload includes the `contactType` and `channelType` fields. Digital interactions do not emit recording-oriented webhook events for transcript readiness.

<a id="capture-available"></a>

### Capture Available

`capture:available`

**Resource Version: capture:1.0.0**

An event indicating that the recording for a call is available after the call has ended.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The task ID associated with the capture. | `"8e18afdf-db79-449b-b4f5-ee4f14d9f45e"` |
| `filePath` | `string` | The file path of the recording. | `"https://api.wxcc-us1.cisco.com/v1/captures/query"` |
| `createdTime` | `integer` | The time that the capture event occurred in epoch milliseconds. | `160266966391` |

<a id="recording-available"></a>

### Recording Available

`recording:available`

**Resource Version: recording:1.0.0**

An event indicating that the recording for an interaction is available. This event is additive to `capture:available` and uses the same general payload structure with additional `contactType` and `channelType` fields.

When the beta additive events are enabled for your organization, a recording-ready voice interaction emits both `capture:available` and `recording:available`. These two events share the same event `id` because they fan out from the same internal recording-ready signal.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The task ID associated with the recording. | `"e7506dab-4430-4d1b-8834-e994c9862eed"` |
| `filePath` | `string` | The Captures API path that the integration should use to retrieve the available recording details for the task. | `"https://api.wxcc-us1.cisco.com/v1/captures/query"` |
| `contactType` | `string` | The media family for which the recording is available. | `"telephony"` |
| `channelType` | `string` | The channel type for which the recording is available. | `"telephony"` |
| `createdTime` | `integer` | The time that the recording event occurred in epoch milliseconds. | `1781593896741` |

<a id="transcription-available"></a>

### Transcription Available

`transcription:available`

**Resource Version: transcription:1.0.0**

An event indicating that the transcript for an interaction is available. This event is additive and does not change the existing meaning of `capture:available`.

For voice and digital interactions, more than one `transcription:available` event can be delivered if more than one transcript artifact becomes available for the same task.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `taskId` | `string` | The task ID associated with the transcript. | `"e7506dab-4430-4d1b-8834-e994c9862eed"` |
| `filePath` | `string` | The Captures API path that the integration should use to retrieve the available transcript details for the task. | `"https://api.wxcc-us1.cisco.com/v1/captures/query"` |
| `contactType` | `string` | The media family for which the transcript is available. This is `telephony` for voice transcripts and can be a digital channel family or admin-configured digital channel value for digital transcripts. | `"telephony"` |
| `channelType` | `string` | Indicates the channel type of a task. | `"telephony", "chat", "email", "social", "customMessaging"` |
| `createdTime` | `integer` | The time that the transcript event occurred in epoch milliseconds. | `1781594954447` |

For capture recovery, consult [Search](https://developer.webex.com/docs/api/v1/search/search) and [List Captures](https://developer.webex.com/docs/api/v1/captures/list-captures).

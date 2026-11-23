---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Flows
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks-cc). [Full Markdown](../../../../docs/webhooks-cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Contact Center webhook event types, resource versions, and event-specific payload fields.

---

<a id="using-webhooks"></a>

<a id="overview"></a>

## Selected section

## Flows

The flow resource represents a published Webex Contact Center Flow Designer execution. A flow defines the routing and orchestration logic that runs for a customer interaction, including IVR prompts, queueing decisions, data dips, virtual agent steps, event handling, and downstream routing actions.

| Resource | Event | Trigger | Resource version |
| --- | --- | --- | --- |
| `flow` | [`flow:error`](https://developer.webex.com/docs/webhooks-cc#flow-error) | A Flow Designer flow encountered an error during execution. | `flow:1.0.0` |

Flow webhooks provide observability events for flow execution outcomes. The `flow:error` webhook is sent when a flow encounters an error during execution. This event is designed for failure scenarios and helps administrators and developers monitor failed flow executions, investigate issues faster, and take action when a flow fails.

The `flow:error` webhook delivers targeted error observability data that can be sent to platforms such as Splunk or other third-party analytics and observability solutions. It is not intended to stream all flow debug or execution data. Use this webhook to monitor actionable flow failures in near real time and to trigger downstream alerting, investigation, or automation workflows.

Customers can manage HTTPS webhook collector URLs in **Developer Portal > Webhooks** to support secure delivery of flow error events to external observability platforms.

<a id="flow-error"></a>

### Flow Error

`flow:error`

**Resource Version: flow:1.0.0**

An event indicating that a Flow Designer flow encountered an error during execution.

Use this event to observe failed flow executions, correlate failures to affected interactions, and route failure details into external observability tools. This event is emitted only for flow failure scenarios and does not include complete flow debug traces or all activity-level execution data.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `interactionId` | `string` | The ID associated with the interaction in which the flow error occurred. | `"44af0d2a-2ef4-4049-a402-e41939d72f4d"` |
| `flowId` | `string` | The ID associated with the flow that encountered the error. | `"684a72233daf36734cb5c499"` |
| `flowVersionId` | `string` | The ID associated with the published flow version that was executing when the error occurred. | `"68510a9f3daf36734cb5c72b"` |
| `tagName` | `string` | The flow tag associated with the executing flow version. | `"Latest"` |
| `activityName` | `string` | The name of the Flow Designer activity where the error occurred. | `"GetQueueInfo_hdt"` |
| `startTime` | `integer` | The time at which the failed activity started, in epoch milliseconds. | `1750855852249` |
| `endTime` | `integer` | The time at which the failed activity ended, in epoch milliseconds. | `1750855852376` |
| `status` | `string` | The flow execution status for this event. | `"error"` |
| `statusDescription` | `string` | The description or reason associated with the error status. | `"INSUFFICIENT_DATA"` |
| `debugUrl` | `string` | The URL that can be used to open the failed interaction in Flow Designer debug mode. | `"https://flow-control.prodjp1.ciscoccservice.com/flow/{flowId}/debug/{interactionId}?orgId={orgId}&version={flowVersionId}"` |
| `createdTime` | `integer` | The time at which the flow error event was created, in epoch milliseconds. | `1750855852391` |

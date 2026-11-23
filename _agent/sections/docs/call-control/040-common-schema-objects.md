---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Schema Objects
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Common Schema Objects

<a id="party-information"></a>

### Party Information

Information about a call party (caller or callee).

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `name` | string | The party's name. Only present when available and privacy is not enabled. |
| `number` | string | The party's number (digits or URI). Only present when available and privacy is not enabled. |
| `personId` | string | The party's person ID. Only present for Webex users when privacy is not enabled. |
| `placeId` | string | The party's place ID. Only present for workspaces when privacy is not enabled. |
| `virtualLineId` | string | The party's virtual line ID. Only present for virtual lines when privacy is not enabled. |
| `id` | string | The party's ID. Only present when available and privacy is not enabled. |
| `idType` | string | Type of ID: `PEOPLE`, `PLACE`, or `VIRTUAL_LINE`. |
| `privacyEnabled` | boolean | Indicates whether privacy is enabled for name, number, and IDs. |
| `callType` | string | Call type: `location`, `organization`, `external`, `emergency`, `repair`, or `other`. |

<a id="redirection-information"></a>

### Redirection Information

Information about a call redirection.

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `reason` | string | Redirection reason: `busy`, `noAnswer`, `unavailable`, `unconditional`, `timeOfDay`, `divert`, `followMe`, `huntGroup`, `callQueue`, or `unknown`. |
| `redirectingParty` | object | Details of the party who redirected the call (see <a href="https://developer.webex.com/docs/call-control#party-information">Party Information</a>). |

<a id="redirect-information"></a>

### Redirect Information

Information about a redirect action.

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `destination` | string | The destination for the redirect (digits or URI). |
| `reason` | string | The reason for the redirect. |
| `redirectTime` | string | The time at which the redirect took place. |

<a id="wrap-up-details"></a>

### Wrap-Up Details

Additional details when an agent enters wrap-up state.

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueId` | string | The queue ID the call was received on. |
| `queueName` | string | The queue name the call was received on. |
| `queueNumber` | string | The queue number the call was received on. |
| `callSessionId` | string | The call session identifier. |
| `wrapUpChangeId` | string | An arbitrary string that changes when the list of available wrap-up codes changes. |
| `maxWrapUpEndTime` | string | The timestamp for max end time for wrap-up. |
| `remoteParty` | object | The details of the party calling the call queue (see <a href="https://developer.webex.com/docs/call-control#party-information">Party Information</a>). |

<a id="call-update-reason-enum"></a>

### Call Update Reason Enum

Reasons for a `callUpdated` event in the queue.

| **Value** | **Description** |
|-----------|-----------------|
| `Call Transferred` | The call was transferred. |
| `Call Picked-Up` | The call was picked up. |
| `Call Barged-In` | The call was barged into. |
| `Call Monitored` | The call was monitored. |
| `Call Forwarded` | The call was forwarded. |
| `Call Park Retrieved` | The call was retrieved from park. |
| `Unknown` | The reason is unknown. |

<a id="overflow-reason-enum"></a>

### Overflow Reason Enum

Reasons for a `callOverflowed` event.

| **Value** | **Description** |
|-----------|-----------------|
| `size` | The queue overflowed due to reaching maximum size. |
| `time` | The queue overflowed due to maximum wait time being exceeded. |

<a id="treatment-completion-reason-enum"></a>

### Treatment Completion Reason Enum

Reasons for treatment completion events (e.g., `callForwardedTreatmentCompleted`, `holidayPolicyTreatmentCompleted`).

| **Value** | **Description** |
|-----------|-----------------|
| `EOF` | The treatment announcement completed normally (end of file). |
| `remoteRelease` | The remote party released the call before the treatment completed. |

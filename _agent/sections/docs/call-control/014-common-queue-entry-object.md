---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queue
- Common Queue Entry Object
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Parent context

## Webhook Payload Schemas

This section provides detailed schema information for each telephony webhook resource.

### telephony_queue

Notification of call queue calls progression.

## Selected section

#### Common Queue Entry Object

Most queue events include a `queueEntry` object with the following fields:

| **Field** | **Type** | **Description** |
|-----------|----------|------------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue (DNIS). |
| `remoteParty` | object | Information about the remote party (see <a href="https://developer.webex.com/docs/call-control#party-information">Party Information</a>). |
| `origCallId` | string | The original call ID for the queue entry. Only present when the queue entry's call ID has changed due to a scenario such as callback where a new call replaces the original call. |
| `addTime` | string | The time when this entry was added to the queue. |
| `removeTime` | string | The time when this entry was removed from the queue. |
| `priority` | string | Priority: `highest`, `high`, `medium`, or `low`. Only present for premium call centers. |
| `bounced` | boolean | Present and true when the call has been bounced one or more times. |
| `reordered` | boolean | Present and true when the call has been reordered within the queue. |
| `mandatoryEntrance` | boolean | Present and true when the call is being played the mandatory entrance message. |
| `preservedWaitTime` | integer | The total time in milliseconds spent waiting in previous queue(s) when transferred. Only present when applicable. |
| `addTimeInPriorityBucket` | string | The time this entry was added to the priority bucket in the queue. |
| `preservedWaitTimeInPriorityBucket` | integer | The preserved wait time in milliseconds this entry has accumulated when being inserted in the priority bucket. Only present when applicable. |
| `answeringAgentId` | string | The ID of the agent that answered the call. Only present when the call is answered. |
| `answeringAgentType` | string | Type of agent: `PEOPLE`, `PLACE`, or `VIRTUAL_LINE`. Only present when the call is answered. |
| `answeringCallId` | string | The call ID of the agent call when answered. Only present for non-distributed calls. |
| `answeringNetworkCallId` | string | The SIP call ID of the agent call when answered. Only present for distributed calls where the call offer from the call queue to the agent contains a SIP call leg. |

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webhook Payload Schemas
- telephony_queue
- Event Types
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

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `callAbandoned` | A call is abandoned by the caller and removed from the queue |
| `callAdded` | A call is added to the queue |
| `callAnsweredByAgent` | A call has been answered by an agent and removed from the queue |
| `callBounced` | A call is bounced back to the queue after being offered to an agent |
| `callEscaped` | The caller dials the configured escape digits while in the queue |
| `callForwarded` | The forced forwarding policy is triggered for a call |
| `callForwardedTreatmentCompleted` | The announcement is completed for a call treated according to the Forced Forwarding policy |
| `callOfferedToAgent` | A call is offered to an agent. The call remains in the queue until answered |
| `callOverflowed` | The overflow policy is triggered for a call in the queue |
| `callOverflowedTreatmentCompleted` | The announcement is completed for a call treated according to the Overflow policy |
| `callPromoted` | A call has been promoted to a different priority in the queue |
| `callReleased` | A call is released from the queue |
| `callReordered` | A call is reordered within the queue |
| `callStranded` | A call is identified as stranded and removed from the queue |
| `callStrandedTreatmentCompleted` | The announcement is completed for a call treated according to the Stranded call policy |
| `callStrandedUnavailable` | A call is identified as stranded due to agent unavailability |
| `callStrandedUnavailableTreatmentCompleted` | The announcement is completed for a call treated according to the Stranded - Unavailable call policy |
| `callTransferred` | A call is transferred to a new destination and removed from the queue |
| `callUpdated` | The remote party attributes are modified while the call is in the queue |
| `holidayPolicyApplied` | The Holiday policy is triggered for a call |
| `holidayPolicyTreatmentCompleted` | The announcement is completed for a call treated according to the Holiday policy |
| `nightPolicyApplied` | The Night policy is triggered for a call |
| `nightPolicyTreatmentCompleted` | The announcement is completed for a call treated according to the Night policy |
| `whisperStarted` | An agent answers an offered call and the whisper announcement is started |

<a id="common-queue-entry-object"></a>

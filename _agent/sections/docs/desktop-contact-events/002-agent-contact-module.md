---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Contact Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-contact-events). [Full Markdown](../../../../docs/desktop-contact-events.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Subscribe to Desktop contact events and use their payloads to keep widgets synchronized with interactions.

## Selected section

## Agent Contact Module

The `Desktop.agentContact` module makes requests and listens to notification events related to the agent-contact entity, such as the arrival of a new task.

**Example**

The [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference#methods-and-properties) lists the contact methods and links to their request payloads. Subscribe to the events your widget needs, and keep the handler reference so you can remove it when the widget disconnects.

```javascript
const onAssigned = message => console.log(message);
Desktop.agentContact.addEventListener("eAgentContactAssigned", onAssigned);

// When the widget disconnects:
function cleanupAssignedListener() {
  Desktop.agentContact.removeEventListener("eAgentContactAssigned", onAssigned);
}
```

**Example Response**

```typescript
// Common fields in contact-event data. Fields vary by event and may be absent.
type AgentContactEventData = {
    mediaResourceId?: string;
    eventType?: string;
    agentId?: string;
    destAgentId?: string | null;
    trackingId?: string;
    consultMediaResourceId?: string | null;
    interaction?: {
        isFcManaged?: boolean;
        isTerminated?: boolean;
        mediaType?: "email" | "chat" | "telephony" | "social" | "sms" | "facebook" | string;
        previousVTeams?: string[];
        state?: string;
        currentVTeam?: string;
        participants?: Record<string, unknown>;
        interactionId?: string;
        orgId?: string;
        owner?: string;
    },
    interactionId?: string;
    orgId?: string;
    owner?: string;
    queueMgr?: string;
    type?: string;
    ronaTimeout?: number;
    isConsulted?: boolean;
    isConferencing?: boolean;
    updatedBy?: string;
    destinationType?: string;
}
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-contact-events
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Additional Contact Events in SDK 3
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-contact-events). [Full Markdown](../../../../docs/desktop-contact-events.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Subscribe to Desktop contact events and use their payloads to keep widgets synchronized with interactions.

## Selected section

## Additional Contact Events in SDK 3

The SDK 3.0.1 declarations also expose the following events. Their callback payload uses `Service.Aqm.Contact.AgentContact` from the SDK types package; TypeScript infers the payload when you pass a callback to `addEventListener`. Inspect the fields supplied for the event before reading optional data.

### eAgentCampaignContactUpdated

Campaign contact information changes. Use the payload to refresh campaign-related widget data. Subscribe with `Desktop.agentContact.addEventListener("eAgentCampaignContactUpdated", handler)` and remove the same handler when the widget disconnects.

### eContactOwnerChanged

Contact ownership changes. The payload may include `fromOwner` and `toOwner` identifiers. Subscribe with `Desktop.agentContact.addEventListener("eContactOwnerChanged", handler)` and remove the same handler when the widget disconnects.

### eParticipantJoinedConference

A participant joins a conference. The payload may include the joined `participantId`. Subscribe with `Desktop.agentContact.addEventListener("eParticipantJoinedConference", handler)` and remove the same handler when the widget disconnects.

### eAgentConsultConferencing

A consultation is transitioning to a conference. Subscribe with `Desktop.agentContact.addEventListener("eAgentConsultConferencing", handler)` and remove the same handler when the widget disconnects.

### eAgentConsultTransferring

A consultation is transitioning to a transfer. Subscribe with `Desktop.agentContact.addEventListener("eAgentConsultTransferring", handler)` and remove the same handler when the widget disconnects.

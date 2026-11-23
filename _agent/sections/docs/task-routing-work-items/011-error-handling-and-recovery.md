---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Error handling and recovery
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/task-routing-work-items). [Full Markdown](../../../../docs/task-routing-work-items.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md)

## Article introduction

Work Items enable external systems to inject non-conversational tasks into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

Availability for Work Items is currently open for **BETA**. Contact your Cisco team to request access.

## Selected section

## Error handling and recovery

Partners should treat `task:failed` and `task-message:append-failed` as the main partner-visible failure events.

**Important guidance:**  

- `task:failed` is the partner-visible failure event for create-task failures
- `task-message:append-failed` is the partner-visible failure event for Work Item update failures
- Representative update-failure reasons include `INVALID_CONTENT`, `INTERNAL_ERROR`, and `NOT_FOUND`

**For request recovery:**

- Validate `destination.id`, `channelType`, `channel`, and `workItemData` before retrying
- Verify the task identifier before retrying Work Item updates
- Correct schema validation failures before retrying
- Retry transient failures with backoff

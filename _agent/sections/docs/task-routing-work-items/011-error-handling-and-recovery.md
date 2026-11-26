---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Error handling and recovery
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/task-routing-work-items). [Full Markdown](../../../../docs/task-routing-work-items.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md)

## Article introduction

Work Items enable external systems to inject **non-conversational tasks** into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

---

New

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

## Selected section

## Error handling and recovery

Partners should handle both HTTP request failures and asynchronous notifications.

**Important guidance:**

- `task:failed` reports task-creation failures after acceptance.
- `task-message:append-failed` reports Work Item update failures after acceptance.
- A successful HTTP submission does not guarantee successful task creation or update.
- Representative update-failure reasons include `INVALID_CONTENT`, `INTERNAL_ERROR` and `NOT_FOUND`. Use `reason` and `errorMessage` to investigate the failure.

**For request recovery:**

- Validate `destination.address`, `channelProperties.channelType`, `channelProperties.channel` and `channelProperties.message.workItemData` before retrying.
- Verify the task identifier before retrying Work Item updates.
- Correct schema validation failures before retrying. Include every required field when creating a task; for updates, check the required fields you supplied.
- When `CONVERSATION_ALREADY_OPEN` is reported, use the existing task for updates instead of creating another task for the same origin and destination.
- Retry transient failures with backoff and correlate responses with their notifications.

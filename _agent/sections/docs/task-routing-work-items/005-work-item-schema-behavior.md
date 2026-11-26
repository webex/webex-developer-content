---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Work Item schema behavior
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

## Work Item schema behavior

The Work Item asset schema defines the metadata fields used when creating or updating a Work Item. Send the data as a JSON object at `channelProperties.message.workItemData`.

For Work Item API requests:

- `workItemData` must be a nonempty object whose values are strings. Do not send numbers, booleans, nested objects, arrays or null as field values.
- Include at least one field defined in the Work Item asset schema.
- **Create Task:** Include every required schema field with a nonempty string value.
- **Task Messages:** Supply the fields you want to update. A payload can contain only an optional schema field. You do not need to repeat required fields that are unchanged. If you include a required field, its value must be nonempty.
- Updates are validated against the schema associated with the existing Work Item.

The following limits apply to each `workItemData` object in an API request:

| Limit | Maximum |
| --- | --- |
| Number of fields | 50 |
| Field key length | 100 UTF-8 bytes |
| Field value length | 1,024 UTF-8 bytes |

UTF-8 byte length can exceed the number of visible characters for non-ASCII text. These limits apply in addition to the configured schema requirements.

Work Items support inbound task creation and metadata updates. Attachments and conversational messaging are not supported.

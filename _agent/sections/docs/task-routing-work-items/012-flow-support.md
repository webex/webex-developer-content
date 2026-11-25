---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Flow Support
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

## Flow Support  

Work Item flows support self-service and routing activities that apply to non-conversational tasks.

Supported Work Item flow activities include:

- `Wait`
- `BRE Request`
- `Condition`
- `Go To`
- `HTTP Request`
- `Case`
- `Parse`
- `End Flow`
- `Percent Allocation`
- `Set Variable`
- `Business Hours`
- `Screen Pop`
- `Set Contact Priority`
- `Escalate CDG`
- `Get Queue Info`
- `Advanced Queue Info`
- `Queue Contact`
- `Queue To Agent`

**Note:** 

- Work Item Start node variables include interaction, entry point, organization, flow, origin, destination and media payload details. The `MediaPayload` object contains the initial Work Item message envelope, including `message.workItemData`. Successful inbound `task-message:appended` notifications contain message metadata and omit `message.workItemData`.
- Call handling activities are not shown in Work Item flows. Custom Messaging Send and Receive nodes are not shown in Work Item flows.

### Start Node Payload And Parse Settings

The following example shows the `MediaPayload` object for the creation request above:

```json
{
  "channelType": "workItem",
  "channel": "ClaimsReview",
  "message": {
    "messageId": "22222222-2222-4222-8222-222222222222",
    "aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
    "direction": "inbound",
    "type": "work-item",
    "workItemData": {
      "customerAccountId": "account-001",
      "customerAccountName": "Customer Name",
      "claimNumber": "CLM-001",
      "priority": "High",
      "claimStatus": "New"
    },
    "timestamp": "2026-05-26T08:51:48.649Z",
    "timestampEpoch": 1779785508649
  },
  "securityComplianceInfo": null
}
```

In the Start node, use Parse settings to extract attributes from the `MediaPayload` object into flow variables. Enter JSON paths relative to that object; there is no separate MediaPayload field to select in Parse settings.

| JSON path | Value to extract |
| --- | --- |
| `$.channel` | Configured Work Item channel name |
| `$.channelType` | `workItem` |
| `$.message.aliasId` | Supplied or generated message alias |
| `$.message.messageId` | Webex message identifier |
| `$.message.workItemData.claimNumber` | Claim number from the configured schema |
| `$.message.workItemData.priority` | Priority field from the Work Item data |
| `$.message.timestampEpoch` | Message time in epoch milliseconds |

Map the extracted attributes to flow variables before using them in routing conditions or later activities. Check that an optional field is present before parsing it. The `securityComplianceInfo` value is always `null` for Work Items.

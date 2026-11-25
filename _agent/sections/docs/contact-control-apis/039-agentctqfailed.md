---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentCtqFailed
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentCtqFailed
This is triggered when a consult-to-queue request fails.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**       | **Description**                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reason`        | Failure reason returned on why the consult-to-queue request failed. Example values:`MaxWaitTimeInQueueExceeded`.                                           |
| `reasonCode`    | Numeric code associated with the failure reason. Example values: `1049` (MaxWaitTimeInQueueExceeded).                                                      |

</details>

```json
{
  "type": "AgentCtqFailed",
  "eventType": "RoutingMessage",
  "interactionId": "e3a50cbc-e494-4207-abe7-34ff92f0713b",
  "orgId": "4df9bd96-7288-44a1-9f1c-40e2038d35b0",
  "queueMgr": "dummy-queue-manager",
  "agentId": "7fd8d46c-8224-4704-89b2-7baa2824fcdf",
  "queueId": "c7d713bd-4dcc-4a28-b8c6-89b7dd0f8fb4",
  "interaction": {...},
  "reason": "MaxWaitTimeInQueueExceeded",
  "reasonCode": 1049,
  "trackingId": "dc177520-12a6-11ee-8eb2-fd656a256ad2",
  "eventTime": 1687622436306
}
```

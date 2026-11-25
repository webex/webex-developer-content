---
type: Guide
title: Task Routing - Work Item
display_title: Task Routing - Work Item
canonical_url: https://developer.webex.com/docs/task-routing-work-items
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/task-routing-work-items)

Work Items enable external systems to inject **non-conversational tasks** into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

---

New

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

## How does this work?

- Developers are expected to host an external system (a middleware) that owns the source task and work item metadata. This is expected to be developed by the partner or customer that integrates with upstream systems and injects tasks into Webex Contact Center.
- Webex Contact Center owns routing, flows, agent handling, task state, lifecycle events, and reporting
- Administrators configure the following entities on **Control Hub** at a high level:
  - **Work Item Channel:** Represents the custom channel that you plan to integrate with (e.g. Fax)
  - **Work Item Asset:** Represents an instance of the channel added above and establishes the data schema payloads you wish to honor when injecting tasks into Webex Contact Center
  - **Flow:** Represents the flow that manages orchestrating a work item and routing it to queues
  - **Queue:** Queues support the `Work Item` channel type
  - **Multimedia Profile:** Determines the no. of tasks an agent can work on in parallel either via automatic contact distribution or self-assignment (cherry picking)
- Developers use **Public APIs** for the following:
  - **Webhook events:** Subscribe to task lifecycle and message events using **Subscriptions API**
  - **Create work item:** Create a work item using **Create Task API v2**
  - **Update work item:** Update a work item's data using **Task Messages API**
  - **Search for work items:** To look up existing work items using **Search API**
  - **Retrieve transcripts:** Pull post interaction transcripts using **Captures API**

## Responsibilities

### External developer

Your **middleware** will be mainly responsible for creating or updating Work Item tasks in Webex Contact Center. Below are the requirements that the developer is expected to manage:

- Hosting the middleware that receives or produces the external work item
- Obtaining and refreshing OAuth tokens to integrate with Webex CC's Task API
- Integration with Webex CC APIs as required - Tasks, Subscription, Search, Captures
- Ensuring that the `Work Item Data` conforms to the administrator-configured Work Item schema on the Asset configured on Control Hub
### Webex Contact Center

Webex Contact Center is responsible for:

- Validating Work Item task requests against configured assets, entry points, and schema
- Running the configured Work Item flow as configured against the Entry point
- Routing Work Items to queues and agents as per the configuration on Webex CC Flow Designer
- Presenting Work Item metadata to agents on the Desktop as read-only data
- Generating task lifecycle and Work Item update webhook events
- Exposing post interaction transcripts for Work Item containing snapshots of the data held within Webex CC.

## Before You Begin

Before integrating, ensure that the administrator has configured the following in Control Hub:

- A `Work Item Custom Channel` with:
  - `Custom channel name`
  - `Logo` (optional)
- A `Work Item Asset` with:
  - `Asset name` and `Description` (optional)
  - `Business address` - Work Item assets use a configured business address to resolve Create Task requests. The business address must be unique across Work Item assets.
  - `Data schema fields` - The schema defines the Work Item metadata fields. Configure at least one required field and one viewable field before saving the asset. API payload limits and the rules for creating and updating these fields are described under [Work Item schema behavior](#work-item-schema-behavior). A schema field includes:
    - `Field key`
    - `Display name`
    - Whether the field is `required`
    - Whether the field is `viewable`
    **Note:** At least 1 viewable and 1 required field is **mandatory**
- A `Work Item Entry Point` mapped to a `Work Item Asset` and a `Work Item Flow`
- `Work Item Queues` and queue ranking within relevant `Teams` as needed
- `Multimedia profile` capacity for Work Items. Please note that we support both **automatic-assignment** and **self-assignment** (cherry picking) similar to other digital channels.
- `RONA timeout` values for Work Items as needed
- Other Contact Center routing objects required for the interaction, such as teams, skills, queues, and agent profiles

## Authenticating APIs

Work Item injection leverages a [Service App](https://developer.webex.com/docs/service-apps) that will represent your middleware so that access token handling is managed appropriately for server-side operations.

For `scope` definitions, refer to [Integration Scopes](https://developer.webex.com/docs/integration-scopes).

### Create and authorize a service app

1. Sign in to the developer portal and create a new **Service App**
2. Capture the client secret when it is first shown. After the app is submitted for authorization, regenerate the secret if it was not saved.
3. Assign the required scopes:
   - `cjp:task_write`
   - `cjp:task_read`
4. Ask the customer administrator to authorize the Service App in Control Hub under **Apps**.
5. After authorization, return to the Service App in the developer portal, select the authorized organization, provide the client secret, and generate the access token.
6. Use the resulting access token when calling the Create Task API and the Task Messages API.

For this integration pattern, ensure that:

- The Service App is authorized for the customer organization
- The `access_token` includes `cjp:task_write` for Create Task and Task Messages
- The `access_token` includes `cjp:task_read` when task read access is required

### Refreshing access tokens  

If your integration needs long-running access, retain the refresh token and use the standard OAuth refresh flow described in the [Authentication guide](https://developer.webex.com/docs/authentication#using-the-refresh-token) before the current access token expires.

For server-to-server integrations, store the `client_secret`, `access_token`, and `refresh_token` securely, and rotate or regenerate credentials according to your organization's security practices.
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

## Subscribe to task and message events

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions) for task lifecycle and Work Item update webhook events. For recommended event types and correlation fields, see [Webhook events](#webhook-events).

## Create a new work item

Use the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task) to create the initial Work Item task.

Send the request to `POST /v2/tasks` using the following request body. This example assumes that the asset schema contains the illustrated fields and that `claimNumber` is required.

**Example request:**

```json
{
  "origin": {
    "address": "crm-lead-10040",
    "name": "Customer Name",
    "type": "customerAddress"
  },
  "destination": {
    "address": "claims-work-items@example.biz",
    "type": "businessAddress"
  },
  "flowSettings": {
    "foo": "bar"
  },
  "globalVariables": {
    "var1": "val1"
  },
  "channelProperties": {
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "message": {
      "aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
      "direction": "inbound",
      "type": "work-item-form",
      "workItemData": {
        "customerAccountId": "account-001",
        "customerAccountName": "Customer Name",
        "claimNumber": "CLM-001",
        "priority": "High",
        "claimStatus": "New"
      },
      "timestampEpoch": 1779785508649
    }
  }
}
```

**Important request fields:**

| Parameter | Description | Mandatory |
| --- | --- | --- |
| `origin.address` | Developer-defined customer, case, task or source-system identifier | Yes |
| `origin.type` | Must be `customerAddress` | Yes |
| `origin.name` | Display name associated with the Work Item origin | No |
| `destination.address` | Business address configured on the Work Item asset | Yes |
| `destination.type` | Must be `businessAddress` | Yes |
| `channelProperties` | Work Item channel and message details | Yes |
| `flowSettings` | Optional flow settings, represented as string key/value pairs | No |
| `globalVariables` | Global variables supplied to the task | No |

Fields inside `channelProperties`:

| Field | Description | Mandatory |
| --- | --- | --- |
| `channelType` | Must be `workItem` | Yes |
| `channel` | Configured Work Item channel name | Yes |
| `message.type` | Must be `work-item-form` | Yes |
| `message.direction` | Must be lowercase `inbound` | Yes |
| `message.aliasId` | Developer-provided message reference, up to 200 characters; it need not be a UUID | No |
| `message.workItemData` | Nonempty string key/value object that satisfies the asset schema, including every required field | Yes |
| `message.timestampEpoch` | Message time as an integer in epoch milliseconds | Yes |

If `aliasId` is omitted, null or empty, Webex Contact Center generates a message alias. Use an integer in epoch milliseconds for `timestampEpoch`, such as the result of JavaScript `Date.now()`.

The Create Task API applies a limit to the complete request body, with a configurable default of 900,000 bytes. A request that exceeds the configured limit is rejected with HTTP 413.

For the full set of supported request combinations and validation rules, refer to the [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task).

**Example response — `202 Accepted`:**

```json
{
  "meta": {
    "orgId": "11111111-1111-4111-8111-111111111111"
  },
  "data": {
    "id": "141897a0-6212-49be-be9d-4823ab1e4dc7"
  }
}
```

Use `data.id` as the created task identifier. Retain this value for subsequent Task Messages API calls and to correlate later task lifecycle subscription webhooks.

`202 Accepted` acknowledges submission; it does not confirm that the Work Item was created. Monitor the task lifecycle events and `task:failed` for the outcome. A successful initial Work Item message also produces a `task-message:appended` notification.

## Update Work Item Data

Use the [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message) to append a metadata update to an existing Work Item.

Send the request to `POST /v2/tasks/{taskId}/messages`, using the task ID returned by Create Task. The channel type and channel must match those used to create the task. This updates Work Item metadata; it does not send a conversational chat message.

The following example updates `claimStatus`. The required `claimNumber` field from the creation example is unchanged, so it does not need to be repeated.

**Example request:**

```json
{
  "channelProperties": {
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "message": {
      "aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
      "direction": "inbound",
      "type": "work-item-form",
      "workItemData": {
        "claimStatus": "Approved"
      },
      "timestampEpoch": 1779789108649
    }
  }
}
```

**Example response — `202 Accepted`:**

```json
{
  "meta": {
    "orgId": "11111111-1111-4111-8111-111111111111"
  },
  "data": {
    "id": "991d52ea-927f-41ff-832b-d8f8601a8fbd"
  }
}
```

Use response `data.id` to correlate the request with the later `task-message:appended` or `task-message:append-failed` notification's `id`. This identifier represents the update event, not the task. A `202 Accepted` response acknowledges submission, not completion of the update.

The following table shows how the `message.aliasId` supplied in a Task Messages request affects the response and notification identifiers. It also shows whether the alias in a successful notification is preserved or generated.

| Request `message.aliasId` | Task Messages response `data.id` and subsequent notification `id` | Successful notification `message.aliasId` |
| --- | --- | --- |
| UUID string | The supplied UUID | The supplied alias |
| Non-UUID string, such as `partner-update-002` | A separately generated UUID | The supplied alias |
| Omitted, null or empty | A separately generated UUID | A generated message alias |

Do not assume that the notification `id`, `message.aliasId` and `message.messageId` always have the same value.

After a successful update, Webex Contact Center publishes the inbound `task-message:appended` subscription webhook for the same Work Item update. See [Webhook events](#webhook-events) for an example.

**Important request fields inside `channelProperties`:**

| Field | Description | Mandatory |
| --- | --- | --- |
| `channelType` | Must be `workItem`, matching the existing task | Yes |
| `channel` | Channel specified in the Create Task request | Yes |
| `message.type` | Must be `work-item-form` | Yes |
| `message.direction` | Must be lowercase `inbound` | Yes |
| `message.aliasId` | Optional developer-provided message reference, up to 200 characters | No |
| `message.workItemData` | Nonempty string key/value object containing the fields to update | Yes |
| `message.timestampEpoch` | Message time as an integer in epoch milliseconds | Yes |

The schema and payload rules under [Work Item schema behavior](#work-item-schema-behavior) also apply here. A channel or channel-type mismatch can be detected after HTTP acceptance and reported through `task-message:append-failed` with reason `INVALID_CONTENT`.

**Common failures**

Common Work Item update failure categories surfaced through `task-message:append-failed` include:

| Failure reason | Typical meaning | Typical next step |
| --- | --- | --- |
| `INVALID_CONTENT` | The update violates schema rules, contains an invalid required-field value, or does not match the task's channel/channel type. | Correct the payload to match the schema and the channel used in Create Task, then retry. |
| `NOT_FOUND` | The referenced task context could not be found. | Verify the task identifier before retrying. |
| `INTERNAL_ERROR` | The platform could not complete the update because of an unexpected internal failure. | Investigate the related failure event and retry. |

These reasons are representative. Some invalid requests are rejected in the HTTP response before acceptance and do not produce an asynchronous failure notification.

### Retry guidance

Assign a UUID to `channelProperties.message.aliasId` for each logical Work Item update and reuse that UUID if the same request needs to be retried. Use a different UUID for each new update. If you retry with the same UUID `aliasId`, the platform reuses that UUID as the API response `data.id` and the corresponding notification `id`. If `aliasId` is omitted, null, empty or not a UUID, the platform generates a new event ID for every request, including retries.

After `202 Accepted`, wait for the matching `task-message:appended` or `task-message:append-failed` notification before deciding whether to retry.

## Webhook events

Use the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions) for task lifecycle and Work Item update webhook events.

Important event families for Work Item integrations include:

- `task:new`
- `task:failed`
- `task-message:appended`
- `task-message:append-failed`

Use the [List Event Types API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions/list-event-types) to discover the latest supported event types and resource versions. Use the [Webhooks guide](https://developer.webex.com/docs/webhooks-cc) for detailed event payload documentation.

A `task-message:appended` notification can acknowledge the initial Work Item message or a subsequent metadata update. Its `data.channelProperties` contains message metadata without `message.workItemData`. The full initial Work Item data is available to the flow through the Start node, as described under [Flow Support](#flow-support). Keep your submitted data if your integration needs to correlate the notification with the field values.

Request messages use `type: "work-item-form"`; returned Work Item message metadata uses `type: "work-item"`.

**Representative Work Item `task-message:appended` subscription webhook for the update above:**

```json
{
  "id": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
  "specversion": "1.0",
  "type": "task-message:appended",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779789109049,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
    "direction": "INBOUND",
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "origin": "crm-lead-10040",
    "destination": "claims-work-items@example.biz",
    "createdTime": 1779789108999,
    "eventDetails": "Appended Work Item data successfully.",
    "channelProperties": {
      "channelType": "workItem",
      "channel": "ClaimsReview",
      "message": {
        "messageId": "44444444-4444-4444-8444-444444444444",
        "aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
        "direction": "inbound",
        "type": "work-item",
        "timestamp": "2026-05-26T09:51:48.649Z",
        "timestampEpoch": 1779789108649
      },
      "securityComplianceInfo": null
    }
  }
}
```

The following table explains the fields in this successful Work Item notification:

| Field | Description |
| --- | --- |
| `id` | Notification identifier; for a Task Messages update, matches the API response `data.id` |
| `data.taskId` | Work Item task identifier returned by Create Task |
| `data.direction` | Direction of the task; `INBOUND` for Work Items |
| `data.channelType` | `workItem` |
| `data.channel` | Configured Work Item channel name |
| `data.origin` | Source-system identifier supplied in `origin.address` when creating the task |
| `data.destination` | Work Item asset business address supplied in `destination.address` |
| `data.createdTime` | Notification creation time in epoch milliseconds |
| `data.eventDetails` | Status summary, when available |
| `data.channelProperties` | Work Item channel and message metadata; excludes `message.workItemData` |
| `data.channelProperties.message.messageId` | Webex message identifier, separate from the alias and notification ID |
| `data.channelProperties.message.aliasId` | Supplied or generated message alias |
| `data.channelProperties.message.direction` | Lowercase `inbound` |
| `data.channelProperties.message.type` | `work-item` |
| `data.channelProperties.message.timestamp` | Original message time in ISO format |
| `data.channelProperties.message.timestampEpoch` | Original message time as an integer in epoch milliseconds |
| `data.channelProperties.securityComplianceInfo` | Always `null` for Work Items. Work Item data is not scanned for PCI or malware. |

**Representative `task:failed` subscription webhook:**

```json
{
  "id": "8be34eb4-d64f-4552-96cc-c9b6e73063c2",
  "specversion": "1.0",
  "type": "task:failed",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": "1779785509049",
  "datacontenttype": "application/json",
  "data": {
    "taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
    "direction": "inbound",
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "origin": "crm-lead-10040",
    "destination": "claims-work-items@example.biz",
    "createdTime": 1779785508999,
    "reason": "ENTRY_POINT_NOT_FOUND",
    "errorMessage": "The Work Item asset does not resolve to an active entry point.",
    "failureType": "failed"
  }
}
```

**Common failures**

Common cases that can result in `task:failed` include:

- `CHANNEL_ASSET_UNDEFINED`: the destination business address does not resolve to a valid Work Item asset
- `FEATURE_FLAG_DISABLED`: the organization is not enabled for Work Items
- `ENTRY_POINT_NOT_FOUND`: the asset does not resolve to an active entry point
- `ORG_DIGITAL_CONTACT_LIMIT_EXCEEDED`: the organization has reached its active digital contact limit
- `CONVERSATION_ALREADY_OPEN`: an active task already exists for the same origin and destination
- `INVALID_CONTENT`: Work Item content validation failed, such as a missing required schema field
- `INTERNAL_ERROR`: an unexpected failure prevented task creation

Some validation or access failures are returned directly in the HTTP response before acceptance. They do not necessarily produce a `task:failed` event.

**Representative `task-message:append-failed` subscription webhook for a request whose channel does not match the task:**

```json
{
  "id": "64ab4f4a-5c93-4339-b325-3878f289a88f",
  "specversion": "1.0",
  "type": "task-message:append-failed",
  "source": "/com/cisco/wxcc/33333333-3333-4333-8333-333333333333",
  "comciscoorgid": "11111111-1111-4111-8111-111111111111",
  "comciscotimestamp": 1779789109049,
  "datacontenttype": "application/json",
  "data": {
    "taskId": "141897a0-6212-49be-be9d-4823ab1e4dc7",
    "direction": "INBOUND",
    "channelType": "workItem",
    "channel": "ClaimsReview",
    "origin": "crm-lead-10040",
    "destination": "claims-work-items@example.biz",
    "createdTime": 1779789108999,
    "reason": "INVALID_CONTENT",
    "errorMessage": "channelProperties.channel must match the channel specified in the Create Task request."
  }
}
```

Failure notifications include `data.reason` for the failure category and `data.errorMessage` for its explanation.

`task-message:append-failed` contains error metadata without `channelProperties`; use its `id` and `data.taskId` for correlation. For task-message notifications, `data.createdTime` is the notification creation time. Message metadata can contain both an ISO `timestamp` and its epoch-millisecond `timestampEpoch`.

In the task-message notifications shown here, `data.direction` is `INBOUND` and nested `message.direction` is lowercase `inbound`. In the `task:failed` example, `data.direction` is lowercase `inbound`.

## Security and data handling  

Work Item webhooks use the same signature, timestamp, replay-protection, and version-header validation model as other Webex Contact Center webhooks. For the generic validation steps, see [Using Webhooks](https://developer.webex.com/docs/using-webhooks).

Work Item metadata can contain customer or business-sensitive data. Partners should:  

- Send only fields required for routing, agent handling, reporting, or downstream processing
- Avoid placing secrets in `workItemData`
- Retain only the task identifiers and correlation identifiers needed for the integration
- Treat `workItemData` as customer data in logs, traces, and analytics stores

`securityComplianceInfo` is always `null` for Work Item messages because Work Item data is not scanned for PCI or malware.

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

## Retrieve Transcripts

Use the [Captures API](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) to retrieve post-interaction transcripts for Work Item tasks.

Work Item transcripts contain metadata snapshots rather than conversational messages. Unlike the notification's message metadata, transcript entries can include `workItemData`.

**Representative Work Item transcript entries:**

The following excerpt shows the identifiers, timestamps and Work Item data for the creation and update examples. Other transcript fields are omitted for clarity.

```json
[
  {
    "id": "22222222-2222-4222-8222-222222222222",
    "aliasId": "51b8f31d-05b2-45f8-b172-63920f2b7d9a",
    "direction": "inbound",
    "workItemData": {
      "customerAccountId": "account-001",
      "customerAccountName": "Customer Name",
      "claimNumber": "CLM-001",
      "priority": "High",
      "claimStatus": "New"
    },
    "timestamp": "2026-05-26T08:51:48.649Z"
  },
  {
    "id": "44444444-4444-4444-8444-444444444444",
    "aliasId": "991d52ea-927f-41ff-832b-d8f8601a8fbd",
    "direction": "inbound",
    "workItemData": {
      "claimStatus": "Approved"
    },
    "timestamp": "2026-05-26T09:51:48.649Z"
  }
]
```

Transcript entry `id` identifies the stored message. Its `aliasId` is the supplied or generated message alias; neither should be assumed to equal the notification event ID.

Work Item transcripts are retrieved after transcript generation, subject to retention and capture availability.

## Related APIs And Guides

- [Authentication guide](https://developer.webex.com/docs/authentication)
- [Integrations guide](https://developer.webex.com/docs/integrations)
- [Create Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/create-task)
- [Task Messages API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/append-task-message)
- [End Task API](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/end-task)
- [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions)
- [List Event Types API](https://developer.webex.com/webex-contact-center/docs/api/v2/subscriptions/list-event-types)
- [Webhooks guide](https://developer.webex.com/docs/webhooks-cc)
- [Using Webhooks](https://developer.webex.com/docs/using-webhooks)
- [Captures API](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures)

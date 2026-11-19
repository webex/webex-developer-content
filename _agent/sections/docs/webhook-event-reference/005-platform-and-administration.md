---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhook-event-reference
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Platform and administration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhook-event-reference). [Full Markdown](../../../../docs/webhook-event-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Webhooks API resources, events, triggers, filters, and links to product-specific payload definitions.

## Selected section

## Platform and administration

`applications` describes application creation, updates, and deletion; `serviceApp` describes authorization and deauthorization. See [their registration requirements](https://developer.webex.com/docs/register-and-manage-webhooks#choosing-applications-vs-serviceapp-webhooks). For a Service App authorization notification, `data.authorizerOrgId` identifies the authorizing customer organization.

| Resource | Event | Trigger | Supported filters |
| --- | --- | --- | --- |
| `dataSources` | `created` | A dataSource was registered. For user-owned registrations, the API accepts `byods:datasource_read`, `spark-admin:datasource_read`, or `spark:all`. Organization-owned registrations require a Full admin with `byods:datasource_read` or `spark-admin:datasource_read`. | `id` — limit to a particular data source, by ID.<br />`schemaId` — limit to a schema id, by ID.<br />`appId` — limit to a particular application id, by ID.<br />`orgId` — limit to a particular organization id, by ID. |
| `dataSources` | `deleted` | A dataSource was deleted. For user-owned registrations, the API accepts `byods:datasource_read`, `spark-admin:datasource_read`, or `spark:all`. Organization-owned registrations require a Full admin with `byods:datasource_read` or `spark-admin:datasource_read`. | `id` — limit to a particular data source, by ID.<br />`schemaId` — limit to a schema id, by ID.<br />`appId` — limit to a particular application id, by ID.<br />`orgId` — limit to a particular organization id, by ID. |
| `dataSources` | `updated` | A dataSource was updated. For user-owned registrations, the API accepts `byods:datasource_read`, `spark-admin:datasource_read`, or `spark:all`. Organization-owned registrations require a Full admin with `byods:datasource_read` or `spark-admin:datasource_read`. | `id` — limit to a particular data source, by ID.<br />`schemaId` — limit to a schema id, by ID.<br />`appId` — limit to a particular application id, by ID.<br />`orgId` — limit to a particular organization id, by ID. |
| `serviceApp` | `authorized` | A Service App that you created was authorized. Use `spark:applications_webhook_write` on the token that creates the webhook. The API also accepts `application:webhooks_write` or `spark:all`. | `id` — limit to this Service App’s application id.<br />`friendlyId` — limit to this Service App’s friendly ID.<br />`trainSiteNames` — limit to Service Apps authorized for this trainSiteName.<br />`adminTrainSiteNames` — limit to Service App authorized for this adminTrainSiteName. |
| `serviceApp` | `deauthorized`| A Service App that you created was deauthorized. Use `spark:applications_webhook_write` on the token that creates the webhook. The API also accepts `application:webhooks_write` or `spark:all`. | `id` — limit to this Service App’s application id.<br />`friendlyId` — limit to this Service App’s friendly ID.<br />`trainSiteNames` — limit to Service Apps deauthorized for this trainSiteName.<br />`adminTrainSiteNames` — limit to Service App deauthorized for this adminTrainSiteName. |
| `applications` | `created` | A Bot, Integration, or Service App was created in your organization. Requires a Full admin with either `spark:applications_webhook_write` or `application:webhooks_write`, and `ownedBy: "org"`. | None |
| `applications` | `updated` | A Bot, Integration, or Service App was updated in your organization. The notification includes an application lifecycle snapshot in `data`; see [Interpret payloads](https://developer.webex.com/docs/webhook-event-reference#interpret-payloads) for its fields. Requires a Full admin with either `spark:applications_webhook_write` or `application:webhooks_write`, and `ownedBy: "org"`. | None |
| `applications` | `deleted` | A Bot, Integration, or Service App was deleted in your organization. Requires a Full admin with either `spark:applications_webhook_write` or `application:webhooks_write`, and `ownedBy: "org"`. | None |
| `adminBatchJobs` | `statusChanged` | A scheduled admin batch job, like “location change”, changed the status. | `jobType` — The job type.<br /><br/>**IMPORTANT**: If you register for a generic webhook without a `jobType` filter, you may receive additional notifications beyond what was scheduled via API and Control Hub. |

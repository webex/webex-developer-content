---
type: Guide
title: Webex Webhooks API | Receive and verify events
display_title: Receive and verify events
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
content_type: documentation
product_group:
- webex-suite
categories:
- admin
- calling
- create
- meeting
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/receive-and-verify-webhooks)

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Before you begin

[Register a webhook](https://developer.webex.com/docs/register-and-manage-webhooks) with a publicly reachable HTTPS destination and a unique secret. Store each registration's ID, secret, expected resource, event, and ownership information. This page covers the Webhooks API; Contact Center Subscriptions use [different envelope and signature rules](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks).

## Handling Requests from Webex

When one of your webhooks is triggered by an event, Webex will send an HTTP POST to the backend `targetUrl` that you've specified. The body of the POST will look something like this:

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svZjRlNjA1NjAtNjYwMi00ZmIwLWEyNWEtOTQ5ODgxNjA5NDk3",
  "name": "New message in 'Project Unicorn' room",
  "resource": "messages",
  "event": "created",
  "filter": "roomId=Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
  "orgId": "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0MyNzljYjMwYzAyOTE4MGJiNGJkYWViYjA2MWI3OTY1Y2RhMzliNjAyOTdjODUwM2YyNjZhYmY2NmM5OTllYzFm",
  "ownedBy": "creator",
  "status": "active",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "data":{
    "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvOTJkYjNiZTAtNDNiZC0xMWU2LThhZTktZGQ1YjNkZmM1NjVk",
    "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
    "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
    "personEmail": "matt@example.com",
    "created": "2015-10-18T14:26:16.000Z"
  }
}
```

The first few properties shown above are called the “envelope.” They identify all webhooks that are sent. This envelope contains the following information:



| Parameter   | Explanation                                                                                                                                                                                                                                                                            |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`        | The webhook ID. This is the same ID returned when you created the webhook and is what you would use to view the webhook configuration or delete the webhook.                                                                                                                           |
| `name`      | The name you gave your webhook when you created it.                                                                                                                                                                                                                                    |
| `resource`  | The resource the webhook data is about.                                                                                                                                                                                                                                                |
| `event`     | The type of event this webhook is for.                                                                                                                                                                                                                                                 |
| `filter`    | Lists any filters that you applied that triggered this webhook.                                                                                                                                                                                                                        |
| `orgId`     | The organization that owns the webhook. This usually is the organization the user that added the webhook belongs to. This ID can be used to [view the Organization details with the API](https://developer.webex.com/docs/api/v1/organizations/get-organization-details).                                                      |
| `createdBy` | The `personId` of the user that added the webhook.                                                                                                                                                                                                                                     |
| `appId`     | The ID of the Webex app that was used to create the webhook. This could be one of your apps, an app from the [Webex App Hub](https://apphub.webex.com), a privately developed app, or this Webex for Developers site if the webhook was created with your personal access token. Webex App Hub is not supported for Webex for Government (FedRAMP). |
| `ownedBy`   | Indicates if the webhook is owned by the *org* or the *creator*. Webhooks owned by the creator can only receive events that are accessible to the creator of the webhook. Those owned by the organization will receive events that are visible to anyone in the organization.          |
| `status`    | Indicates if the webhook is active. A webhook that cannot reach your URL is disabled. Thus, for all webhooks you receive, the status will always read ‘active.’                                                                                                                        |
| `actorId`   | The `personId` of the user that caused the webhook to be sent. For example, on a *messsage created* webhook, the author of the message will be the actor. On a *membership deleted* webhook, the actor is the person who removed a user from a room.                                   |
| `data`      | Contains the JSON representation of the resource that triggered the webhook. **Note:** Use the documented organization field for the operation you are performing. For Service App authorization, use `data.authorizerOrgId` to identify the authorizing customer; see [Service App authorization](https://developer.webex.com/docs/contact-center-service-apps#service-app-creation-developer-flow).                  |

<a id="using-the-data-property"></a>

### Using the Data Property

The webhook's `data` property contains the JSON representation of the resource event that triggered the webhook. For example, if you created a webhook that triggers when `messages` are `created` (i.e. posted into a room), then the `data` property will contain the JSON representation for a message resource, as specified in the [Messages API](https://developer.webex.com/docs/api/v1/messages) documentation.  Likewise, if you created a webhook that triggers when `telephony_calls` are `created` (i.e. a call is originated or received), then the `data` property will contain the JSON representation for a telephony_calls resource, as specified in the [Call-Control API](https://developer.webex.com/docs/api/v1/call-controls) documentation.

If the webhook's resource event contains sensitive data, the data property will only contain “metadata” about the event. See [Handling Sensitive Data](#handling-sensitive-data) for more information about how to retrieve the entire resource.

<a id="handling-sensitive-data"></a>

### Handling Sensitive Data

Webex encrypts sensitive room content such as titles and message text using keys only available to the members of that room. This means that not even the Webex operations team can read your messages, This affects the resource data included in webhook notifications.

You'll notice in the above message webhook example that the `text` property is missing. That's because room messages are considered sensitive information and since Webex initiated the request to your backend, it did not have your Access Token with which to decrypt the message. In order to get the sensitive information, your app needs to use the resource `id` to fetch the full resource. Using the above messages example, your app could fetch the complete message object along with the text by doing an authenticated (via your Bearer Token) GET request to `/messages/{id}` as shown below:

`GET https://webexapis.com/v1/messages/Y2lzY29zcGFyazovL3VzL01FU1NBR0UvMzIzZWUyZjAtOWFhZC0xMWU1LTg1YmYtMWRhZjhkNDJlZjlj`

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvMzIzZWUyZjAtOWFhZC0xMWU1LTg1YmYtMWRhZjhkNDJlZjlj",
  "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
  "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "personEmail": "matt@example.com",
  "text": "Something interesting and potentially sensitive",
  "created": "2015-12-04T17:33:56.767Z"
}
```

<a id="authenticating-requests"></a>

## Authenticating Requests

Webhooks require that the Webex Cloud be able to reach your backend over HTTP. One common question from enterprise IT is how to authenticate that a request is coming from Cisco. We are continuously adding infrastructure to the Webex Cloud so only listing IPs that are allowed is not practical. To solve this, we introduced a technique for cryptographically verifying the JSON payload based on a shared secret of your choosing.

When creating a webhook, supply a unique `secret` parameter for each registration and reject deliveries whose signatures fail verification. When Webex sends a notification for that webhook, the `X-Spark-Signature` HTTP header contains an [HMAC-SHA1](https://en.wikipedia.org/wiki/Hash-based_message_authentication_code) signature computed over the notification's unmodified raw request body.

Supply the `secret` when [registering the webhook](https://developer.webex.com/docs/register-and-manage-webhooks). Store it with the registration ID in your application configuration.

HTTP header names are case-insensitive. Webex may deliver this header in lowercase when using HTTP/2, so use a case-insensitive lookup in your receiver. Compute the HMAC over the raw request bytes before parsing or re-serializing JSON, and compare signatures in constant time before processing the payload. HMAC-SHA1 is described here because it is part of the `X-Spark-Signature` webhook contract, not as a general cryptographic recommendation.

Webex supports these signature headers:

- `X-Spark-Signature` contains an HMAC-SHA1 signature when you create the webhook with a secret. Use it as the compatibility path for webhook types that do not provide the newer signature header.
- `X-Webex-Signature` provides HMAC-SHA256 and HMAC-SHA512 signatures for supported webhook types. Prefer this header when it is available. It contains comma-separated `algorithm=signature` pairs, with the exact algorithm labels `SHA-256` and `SHA-512`.

The `X-Webex-Signature` digest values are lowercase hexadecimal, not Base64: 64 characters for `SHA-256` and 128 characters for `SHA-512`. The header format is:

```http
X-Webex-Signature: SHA-256=<64 hexadecimal characters>, SHA-512=<128 hexadecimal characters>
```

For example, the exact raw body `{"example":"webhook"}` with no trailing newline and the illustrative secret `example-secret` produces:

```http
X-Webex-Signature: SHA-256=c7eeb9578693c5d55a7cdd25c515eec86a8416b47e68c67147f0dd6ad1398e76, SHA-512=261a573b95238d6c46906578453f400f232ff43e19e7500cb0d3062dd620c5e0018049b1d66586eccbf5436d56434ce2bd2f341f6a5605bb11ba5c1afc0e2407
```

This is a synthetic verification example, not a complete Webex event. Use your own unique secret when registering a webhook.

To verify `X-Webex-Signature`, split the header on commas, trim surrounding whitespace from each pair, and split each pair at the first `=`. Select a supported algorithm, such as `SHA-256`, compute its HMAC using the registered secret and raw request body, and compare the resulting digest with that pair's hexadecimal value. Do not compare a single digest with the entire header value. Reject a request if no supported signature verifies.

For either header, compute the HMAC over the same unmodified raw request bytes and compare the expected and received signatures in constant time. Do not parse, re-serialize, or otherwise normalize the JSON before verification.

## Data Synchronization Meetings

We generally provide webhooks that are actionable. This means the webhook has enough information to be useful to drive most workflow scenarios. We have found some customers who want to query additional details from the REST resource after receiving a webhook. The REST resource may not be immediately in sync with the webhook received, which is sent as soon as possible.
Due to a complex multistage backend, our current SLA is a sync between webhook and REST resource within 10 minutes for 99.5% of cases.
Let’s use a practical example. A developer registers for the meetingParticipants:joined webhook. After the webhook is received the developer wants to query the /meetingParticipants/{id} REST resource. This request may return a 404 as long as the REST resource is synching with the subsystems.

## Disabled Webhooks

Webex can disable a webhook after repeated delivery failures, including an unreachable endpoint or an unsuccessful HTTP response. Failure thresholds and the counting interval are configurable; do not depend on a fixed number of attempts as a retry guarantee. Once disabled, a webhook is not reenabled automatically.

To see the current status of a webhook, use the [Get Webhook Details](https://developer.webex.com/docs/api/v1/webhooks/get-webhook-details) API endpoint. To reactivate a disabled webhook, use the [Update a Webhook](https://developer.webex.com/docs/api/v1/webhooks/update-a-webhook) API endpoint with the `status` parameter set to ‘active’.

Correct the delivery failure before reenabling the webhook. Failure counts can remain until their current counting interval expires, so a reenabled webhook can be disabled again quickly if delivery still fails. Reenabling does not guarantee a fresh failure budget.

## Handle duplicate notifications

Your app can receive more than one notification for an event. Make your webhook handler idempotent so processing the same notification again does not repeat a side effect, such as creating a second record or sending a second message. If the documentation for an event defines a stable event identifier, record it durably and check it before applying side effects. Otherwise, make updates safe to repeat and use the event and resource data to determine whether an action is still needed. Durable queues and idempotent processing are common ways to handle webhook delivery safely.

In the Webex webhook envelope, `id` identifies the webhook configuration; it is not a unique event or delivery identifier. Do not use that field by itself to deduplicate events, and do not assume a resource ID identifies a particular event.

## Acknowledge accepted events

Verify the signature and validate the delivery against your stored registration before processing it. Return a successful 2xx response only after processing has completed or durable storage has accepted the event for a worker. Acknowledge durable acceptance separately from completion of the business action. Make worker retries safe to repeat.

Treat payloads as sensitive. Log correlation IDs and outcomes rather than tokens, signing secrets, signatures, or message contents. Track delivery acceptance failures, verification failures, queue backlog, and processing failures in your application.

## Verify your implementation

Use the synthetic body and secret in [Authenticating Requests](#authenticating-requests) only as a local test fixture. Compute the HMAC over the exact bytes, including the absence of a trailing newline, and compare against the documented SHA-256 and SHA-512 values.

Check a valid delivery, then modify its body without updating the signature, remove the signature, provide a malformed digest, and provide an unsupported algorithm label. Invalid requests must stop before a business action or enqueue operation. Test both supported signature contracts that your webhook type actually emits; do not assume every resource sends `X-Webex-Signature`.

Deliver the same event twice and confirm it cannot repeat a side effect. The registration `id` is not a unique event identifier. Confirm that a failed durable acceptance cannot produce a successful acknowledgement.

## Troubleshoot delivery

| Symptom | Check |
| --- | --- |
| No delivery after registration | Confirm the registration is active, the expected event occurred, filters match an accessible resource, and Webex can reach the HTTPS endpoint. For Calling, inspect applicable interest registrations and expiration. |
| Signature mismatch | Use the secret for this registration and the unmodified body bytes. Look up header names case-insensitively. Parse the newer header's algorithm/digest pairs instead of comparing a digest to the whole header. |
| Message text is absent | Fetch the resource with your application token; see [Handling Sensitive Data](#handling-sensitive-data). |
| A Meeting REST lookup returns 404 after an event | See [Data Synchronization Meetings](#data-synchronization-meetings) before treating the resource as absent. |
| Duplicate actions | Inspect the idempotency strategy and durable worker state. Do not deduplicate all events using the registration ID. |
| Deliveries stopped after endpoint failures | Inspect status and follow [Disabled Webhooks](#disabled-webhooks). Correct the endpoint failure before reenabling delivery. |

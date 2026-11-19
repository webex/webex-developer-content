---
type: Guide
title: Contact Center Webhooks | Receive and verify events | Move 6c58a4ceb0fb
display_title: Receive and verify events
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
content_type: documentation
product_group:
- webex-contact-center
categories:
- create
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks)

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Before you begin

[Create and manage a subscription](https://developer.webex.com/docs/using-webhooks#customer-onboarding-page) with a unique secret and a publicly reachable HTTPS receiver. Your application must store each subscription's ID, customer organization, secret, API version, and configured resource version. See [Register and manage subscriptions](https://developer.webex.com/docs/using-webhooks) for registration and V1-to-V2 migration, and [Event reference](https://developer.webex.com/docs/webhooks-cc) for resource versions and event-specific data.

This page covers Contact Center Subscriptions webhooks. For Messaging, Meetings, Calling, and administration events registered with the Webhooks API, use the [Webex Webhooks API receiver guide](https://developer.webex.com/docs/receive-and-verify-webhooks); its signature headers and envelope are different.

## Receiving Webhooks

We draw inspiration from the CloudEvents.io [JSON format](https://github.com/cloudevents/spec/blob/v1.0.1/json-format.md#32-examples), [HTTP Structured Content Mode](https://github.com/cloudevents/spec/blob/v1.0.1/http-protocol-binding.md#32-structured-content-mode), and [Webhook](https://github.com/cloudevents/spec/blob/v1.0.1/http-webhook.md) specifications. The main areas in which we differ are Webhook authorization, and managing request rates and 429s.

If you are not familiar with CloudEvents spec, do not worry. Here's what you need to know:

<a id="anatomy-of-a-webhook"></a>

## Anatomy of a Webhook

We send POST requests to the destinationUrl of the Subscription. The following cURL requests illustrate the V1 and V2 headers and body shapes. For **both versions**, replace the signature with an HMAC-SHA256 hex digest computed over the exact body bytes using the secret in your test subscription registry. The displayed signatures are not valid for a secret you choose. For V2, update both timestamps before computing that digest.

__Version 1.0 subscription__
```bash #curl_v1
curl \
    -X POST \
    http://localhost:1337/v1/notifications \
    -H "content-type: application/json" \
    -H "user-agent: " \
    -H "X-WebexCC-Signature: 227c6b5aeb154b9d034aadd65fbc50f1dfa6dd5f91feb7f7c91f9449e3730285" \
    -H "connection: keep-alive" \
    --data-raw '{"comciscoorgid":"3eb3c4b5-6c60-4893-8bd8-8454537324e4","data":{"...":"..."},"datacontenttype":"application/json","id":"e9619c7b-8f8a-45e6-9f32-f44ecef98472","source":"/com/cisco/wxcc/fdcac25f-c5e3-43ba-8455-67c44cf4936c","specversion":"1.0","type":"agent:login"}'
```
__Version 2.0 subscription__

With Version 2.0 based subscription, we add the X-WebExCC-Timestamp and X-WebexCC-Webhook-Version headers:
```bash #curl_v2
curl \
    -X POST \
    http://localhost:1337/v1/notifications \
    -H "content-type: application/json" \
    -H "user-agent: " \
    -H "X-WebexCC-Signature: a68fac8fcf67a36071139c2808d90965aed73109b1e86386c03802e53fad51bb" \
    -H "X-WebExCC-Timestamp: 1697211697694" \
    -H "X-WebexCC-Webhook-Version: agent:1.0.0" \
    -H "connection: keep-alive" \
    --data-raw '{"comciscoorgid":"3eb3c4b5-6c60-4893-8bd8-8454537324e4","comciscotimestamp": "1697211697694","data":{"...":"..."},"datacontenttype":"application/json","id":"e9619c7b-8f8a-45e6-9f32-f44ecef98472","source":"/com/cisco/wxcc/fdcac25f-c5e3-43ba-8455-67c44cf4936c","specversion":"1.0","type":"agent:login"}'
```
Note: When testing the sample code below with a 2.0 payload, the above curl command includes an expired timestamp. Consequently, upon running the code, you will encounter a validation error message. To resolve this, replace the outdated `X-WebExCC-Timestamp` and `comciscotimestamp` with the current Unix timestamp. After that, generate a new hash for the `X-WebexCC-Signature` and update it in the curl request to successfully pass the replay attack validation step.

The request body follows this structure:

__For Version 1.0 based subscription__
```json #json_v1
{
    "comciscoorgid": "3eb3c4b5-6c60-4893-8bd8-8454537324e4",
    "data": {
        "...": "..."
    },
    "datacontenttype": "application/json",
    "id": "e9619c7b-8f8a-45e6-9f32-f44ecef98472",
    "source": "/com/cisco/wxcc/fdcac25f-c5e3-43ba-8455-67c44cf4936c",
    "specversion": "1.0",
    "type": "agent:login"
}
```

__For Version 2.0 based subscription__
```json #json_v2
{
    "comciscoorgid": "3eb3c4b5-6c60-4893-8bd8-8454537324e4",
    "comciscotimestamp": "1697211697694",
    "data": {
        "...": "..."
    },
    "datacontenttype": "application/json",
    "id": "e9619c7b-8f8a-45e6-9f32-f44ecef98472",
    "source": "/com/cisco/wxcc/fdcac25f-c5e3-43ba-8455-67c44cf4936c",
    "specversion": "1.0",
    "type": "agent:login"
}
```

The JSON body shown above is an envelope around the `data` field, which varies by the event type. The envelope follows the [CloudEvents.io JSON format](https://github.com/cloudevents/spec/blob/v1.0.1/json-format.md#32-examples). Here's what they mean:

- `id`: Unique per source event (but not per notification; one source event may trigger multiple notifications). You may use this for event deduplication.
- `source`: Contains the Subscription ID at the end.
- `type`: The type of event (indicated as eventType in the Subscription API).
- `specversion`: The CloudEvents envelope version, `1.0`.
- `datacontenttype`: The event data content type, `application/json`.
- `campaignId`: (only provided for campaign events) The ID of the campaign.
- `comciscoorgid`: Org ID of the organization where the event occurred.
- `comciscotimestamp`: (Version 2.0+) The UTC time in epoch ms that the request body is constructed. Should match `X-WebExCC-Timestamp` header.

The request will be made only over HTTPS with a valid certificate using TLS. Self-signed certificates will not work. When you first start development, a tool such as [ngrok](https://ngrok.com/) can help you get past this requirement.

## Delivery, ordering, and reconciliation

Contact Center integrations should reconcile webhook-driven state with the relevant resource APIs. Delivery can be missed. Choose a reconciliation schedule and query windows appropriate to the resource and your application; consult resource-specific recovery APIs in the [event reference](https://developer.webex.com/docs/webhooks-cc).

Contact Center events can arrive out of order. Check resource state and event timestamps before applying stateful updates. Do not assume arrival order represents resource state order.

See [Handle duplicate deliveries](#handle-duplicate-deliveries) for source-event identifiers and the durable acceptance boundary.

<a id="not-receiving-events"></a>

## Not Receiving Events?

Double-check:

- Events in Webex Contact Center are occurring.
- The subscription exists, is enabled, and has the correct `destinationUrl`.
- Your company/datacenter firewall could be blocking incoming HTTPS requests. Please note that we cannot provide IT with static IPs, as our cloud infrastructure is dynamic in nature.

<a id="request-verification"></a>

## Request Verification

To verify requests are originating from Webex Contact Center, are authentic, and are unmodified, you may verify webhooks using a cryptographic signature. Receivers are strongly encouraged to implement this feature for their own security.

When a Subscription is registered, a `secret` may be provided. Providing a `secret` causes our system to include the `X-WebexCC-Signature` header in webhooks. To verify a webhook, you must supply the unmodified request body and Subscription's secret to the HMAC-SHA256 algorithm, then compare the hex-encoded output with the header's value in constant time. Reject a missing, malformed, or invalid signature before processing the event. If they match, then the webhook is valid. Note that this system relies on the provided `secret` field being confidential.

Built-ins or packages exist for most language ecosystems for taking HMAC signatures. The sample code, below, implements this check in Node.

<a id="replay-attack-prevention-20-based-subscriptions-only"></a>

## Replay attack prevention (2.0 based subscriptions only)

For V2 based subscriptions, we provide a timestamp indicating when the event was dispatched, as a part of body `comciscotimestamp` and header `X-WebExCC-Timestamp`. This timestamp, in conjunction with HMAC signatures, gives a way to validate when the event was sent out, and mitigate replay attacks.

After verifying the HMAC over the raw request bytes, require the timestamp header to match the signed timestamp in the body. Reject missing, malformed, mismatched, expired, or excessively future-dated timestamps. Choose a clock tolerance appropriate to your application; the example below uses five minutes in either direction. Determine whether V2 checks are required from your stored subscription configuration, rather than the presence of an incoming header. Keep receiver clocks synchronized. Timestamp validation limits replay age; it does not replace durable event deduplication within that window.

The sample code below contains a way to check this.

<a id="identifying-event-version-20-based-subscriptions-only"></a>

## Identifying event version (2.0 based subscriptions only)

With V2 based subscriptions, the event request contains the `X-WebexCC-Webhook-Version` header indicating the event resource version. Require that header to match the resource version you stored when registering the subscription before choosing a payload schema or accepting the event. Reject a missing or mismatched value; the HMAC covers the body, not this header.

You would want to migrate your subscription to newer version of events (as and when it's released), to get the best and latest of contact center webhook events. Older version of events will become inactive at some point in time.

<a id="response"></a>

## Response

<a id="code"></a>

### Code

Any 2xx response is acceptable.

Any other response (if there is a response) is considered a failure.

Redirects (3xx or otherwise) are never followed.

<a id="latency"></a>

#### Latency

Must respond within 5 seconds. Consider using a 202 Accepted pattern, where you accept the request and queue the event to be processed elsewhere.

## Handle duplicate deliveries

The envelope's `id` identifies a source event and may be shared by multiple notifications for that event. Use `id` to deduplicate the event across subscriptions, or the `source` and `id` pair to deduplicate repeat deliveries within one subscription. Atomically persist your chosen key with the accepted event, or make your durable queue and worker enforce that scope. Keep downstream side effects idempotent. See [delivery considerations](#delivery-ordering-and-reconciliation) for reconciliation and ordering.

<a id="example-nodejs-app"></a>

## Operate your receiver

Track acceptance latency against the five-second response limit, registry/queue failures, signature and timestamp rejection counts, queue backlog, and worker processing failures. Keep payloads, tokens, secrets, and signatures out of application logs. Use event and subscription IDs for correlation.

A successful acknowledgement means the event was durably accepted. Record business processing completion separately, retry failed work idempotently, and reconcile resource state after missed deliveries or application outages. The API does not provide a universal replay operation for every resource.

## Example Node.js app

This Express example receives JSON at `/v1/notifications`. It verifies the original body bytes before trusting the event's organization, validates V2 timestamps using stored subscription configuration, and returns `202` only after a durable queue accepts the event. Invalid requests stop before enqueueing. It does not log payloads, secrets, or signatures.

Implement `getSubscription` with your trusted subscription registry and secret store. It must return `{orgId, secret, version, resourceVersion}` for an active subscription owned by your application, where `version` is the number `1` or `2` and V2 subscriptions include their configured `resourceVersion` (for example, `agent:1.0.0`); return `null` for an unknown or inactive subscription. A lookup outage should throw so the receiver returns `503`. Implement `enqueueDurably` with a queue provider that confirms persistence before resolving. Its worker must enforce your chosen deduplication scope and process events idempotently. These two integration functions are intentionally unimplemented; the example fails closed until you supply them. Configure registry and queue deadlines so the complete handler responds within the five-second delivery limit.

Use a supported Node.js release and Express. Expose the local listener through a trusted HTTPS endpoint for Webex delivery. Apply ingress rate and body-size limits appropriate to your event payloads; the example sets a 1 MiB limit and does not accept compressed request bodies.

```javascript
const express = require("express");
const crypto = require("node:crypto");

const app = express();
app.disable("x-powered-by");
app.use(express.json({
    limit: "1mb",
    inflate: false,
    verify(req, res, bytes) {
        req.rawBody = Buffer.from(bytes);
    },
}));

app.post("/v1/notifications", async (req, res) => {
    const body = req.body;
    if (!Buffer.isBuffer(req.rawBody) || !body || typeof body !== "object" ||
        Array.isArray(body) || typeof body.source !== "string" ||
        !body.source.startsWith("/com/cisco/wxcc/")) {
        return res.sendStatus(400);
    }
    const subscriptionId = body.source.slice("/com/cisco/wxcc/".length);
    if (!subscriptionId || subscriptionId.includes("/")) {
        return res.sendStatus(400);
    }

    let subscription;
    try {
        subscription = await getSubscription(subscriptionId);
    } catch {
        return res.sendStatus(503);
    }
    if (!subscription) return res.sendStatus(403);
    if (typeof subscription.secret !== "string" || !subscription.secret ||
        typeof subscription.orgId !== "string" || !subscription.orgId ||
        ![1, 2].includes(subscription.version)) {
        return res.sendStatus(503);
    }

    const signature = req.headers["x-webexcc-signature"];
    if (typeof signature !== "string" || !/^[a-fA-F0-9]{64}$/.test(signature)) {
        return res.sendStatus(403);
    }
    const expected = crypto.createHmac("sha256", subscription.secret)
        .update(req.rawBody).digest();
    if (!crypto.timingSafeEqual(Buffer.from(signature, "hex"), expected)) {
        return res.sendStatus(403);
    }
    if (body.comciscoorgid !== subscription.orgId ||
        typeof body.id !== "string" || !body.id ||
        typeof body.type !== "string" || !body.type) {
        return res.sendStatus(403);
    }

    if (subscription.version === 2) {
        if (typeof subscription.resourceVersion !== "string" ||
            !/^[a-z][a-z0-9-]*:\d+\.\d+\.\d+$/.test(subscription.resourceVersion)) {
            return res.sendStatus(503);
        }
        if (req.headers["x-webexcc-webhook-version"] !== subscription.resourceVersion) {
            return res.sendStatus(403);
        }
        const timestamp = req.headers["x-webexcc-timestamp"];
        const sentAt = Number(timestamp);
        if (typeof timestamp !== "string" || !/^\d{1,16}$/.test(timestamp) ||
            String(body.comciscotimestamp) !== timestamp ||
            !["string", "number"].includes(typeof body.comciscotimestamp) ||
            !Number.isSafeInteger(sentAt) ||
            Math.abs(Date.now() - sentAt) > 5 * 60 * 1000) {
            return res.sendStatus(403);
        }
    }

    try {
        await enqueueDurably({
            subscriptionId,
            body,
            resourceVersion: subscription.version === 2 ? subscription.resourceVersion : undefined,
        });
    } catch {
        return res.sendStatus(503);
    }
    return res.sendStatus(202);
});

async function getSubscription(subscriptionId) {
    // Implement an app-owned subscription lookup and secret-store read.
    throw new Error("Subscription registry is not configured");
}

async function enqueueDurably(event) {
    // Resolve only after durable storage; implement idempotent worker processing.
    throw new Error("Durable queue is not configured");
}

app.listen(1337, "127.0.0.1", () => {
    console.log("Webhook receiver is listening behind the HTTPS endpoint");
});
```

## Verify your receiver

Configure a test subscription and secret in your registry. For V1 or V2, compute a fresh HMAC-SHA256 digest over the exact JSON body bytes using that secret and put its hex value in `X-WebexCC-Signature`; do not reuse the illustrative signature above. For V2, first replace both timestamp values with the same current Unix time in milliseconds, then compute the digest over that updated body. Confirm that a valid request is durably accepted before receiving `202`.

Then change the body without recomputing its signature, omit or corrupt the signature, and send mismatched or out-of-window V2 timestamps. Each must stop before enqueueing. Confirm that a registry or queue outage returns `503`, and that duplicate deliveries cannot repeat downstream side effects. Acknowledgement, signature verification, timestamp validation, and deduplication are separate checks.

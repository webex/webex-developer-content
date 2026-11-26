---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Example Node.js app
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

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

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Anatomy of a Webhook
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks). [Full Markdown](../../../../docs/receive-and-verify-contact-center-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Contact Center webhook events, verify their signatures, and acknowledge deliveries after durable acceptance.

## Selected section

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

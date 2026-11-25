---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authenticating Requests
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

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

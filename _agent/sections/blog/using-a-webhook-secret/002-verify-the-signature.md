---
type: Excerpt
canonical_url: https://developer.webex.com/blog/using-a-webhook-secret
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the signature
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/using-a-webhook-secret). [Full Markdown](../../../../blog/using-a-webhook-secret.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

> **Info**
>
> Updated September 2026: This post has been refreshed with current Webex webhook security guidance.



Webhooks send HTTP POST requests to the public URL you provide. A shared secret lets your receiver verify the request before it parses or processes the payload.

## Selected section

## Verify the signature

When a webhook has a secret, Webex includes an `X-Spark-Signature` header containing an HMAC-SHA1 signature of the raw JSON request body. This example uses SHA-1 only because it is part of the Webex webhook contract, not as a general cryptographic recommendation. Header names are case-insensitive, and HTTP/2 clients can deliver the field name in lowercase, so use your framework's case-insensitive header lookup.

Some webhook types also provide HMAC-SHA256 and HMAC-SHA512 signatures in the `X-Webex-Signature` header. Prefer that header when it is available; this example covers the HMAC-SHA1 `X-Spark-Signature` path. See the [API changelog](https://developer.webex.com/docs/api/changelog) for the signature options.

Verify the signature against the raw request bytes before parsing JSON. Compare the expected and received signatures in constant time, then reject the request when the header is missing or does not match.

This Flask example returns `401` for an invalid request and only reaches application logic after verification succeeds:

```python
import hashlib
import hmac
import os
from typing import Optional

from flask import Flask, request

app = Flask(__name__)
WEBHOOK_SECRET = os.environ["WEBEX_WEBHOOK_SECRET"].encode("utf-8")


def is_valid_webhook(raw_body: bytes, received_signature: Optional[str]) -> bool:
    if not received_signature:
        return False

    expected_signature = hmac.new(
        WEBHOOK_SECRET,
        raw_body,
        hashlib.sha1,
    ).hexdigest()
    return hmac.compare_digest(expected_signature, received_signature)


@app.post("/webex-events")
def receive_webhook():
    raw_body = request.get_data()
    signature = request.headers.get("x-spark-signature")

    if not is_valid_webhook(raw_body, signature):
        return "Invalid signature", 401

    # Parse and process raw_body only after signature verification succeeds.
    return "", 204
```

Return a successful 2xx response after you accept the event. Requests that fail verification should not reach the rest of your bot or integration logic. For a broader webhook security example, see [Building a More Secure Bot](https://developer.webex.com/blog/building-a-more-secure-bot).

For the complete webhook API, see the [Webhooks guide](https://developer.webex.com/docs/webhooks).

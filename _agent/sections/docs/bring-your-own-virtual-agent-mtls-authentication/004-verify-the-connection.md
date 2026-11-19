---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the connection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-mtls-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Add optional mutual TLS (mTLS) client authentication to a Bring Your Own Virtual Agent (BYOVA) gRPC endpoint while retaining the existing JWS/JWT validation.

## Selected section

## Verify the connection

Verify all authentication layers before enabling mTLS in production:

1. Connect without a client certificate and confirm that the TLS handshake fails.
2. Connect with a certificate that is not trusted or is not in the configured identity allowlist and confirm that the connection is rejected.
3. Connect with the valid Webex CCAI certificate for the tenant's environment and region and confirm that the TLS handshake succeeds.
4. After the mTLS handshake succeeds, send a request with an invalid JWS/JWT and confirm that the authorization interceptor rejects it.
5. Send a request with both a valid client certificate and valid JWS/JWT, then confirm that the BYOVA gRPC service receives the request.

An mTLS handshake proves the transport peer's certificate identity. The JWS/JWT check separately authorizes the BYOVA request and remains required.

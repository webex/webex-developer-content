---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-mtls-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Add optional mutual TLS (mTLS) client authentication to a Bring Your Own Virtual Agent (BYOVA) gRPC endpoint while retaining the existing JWS/JWT validation.

## Selected section

## Overview

mTLS adds transport-layer authentication in both directions: Webex CCAI validates your gRPC server certificate, and your server validates the client certificate presented by Webex CCAI. The handshake completes before application data is sent.

mTLS is optional and applies only to the gRPC variant of BYOVA. It does not apply to the WebSocket variant. Enabling mTLS does not replace JWS/JWT validation; continue to validate the authorization token on every connection.

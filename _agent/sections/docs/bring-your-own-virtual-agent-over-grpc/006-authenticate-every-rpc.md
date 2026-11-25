---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authenticate every RPC
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Authenticate every RPC

Validate the JWS/JWT from the gRPC `authorization` metadata on every call. At minimum, verify the signature, expiration, issuer, required claims, and that the data source URL and schema claims match the registered connector.

The Java sample includes a complete JWT validation pattern. The Python sample contains an authentication scaffold and must be hardened before production use. Never disable token validation on a publicly reachable endpoint.

For transport-level client authentication in addition to JWS/JWT, see [mTLS Authentication](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication).

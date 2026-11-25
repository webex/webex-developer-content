---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-mtls-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add optional mutual TLS (mTLS) client authentication to a Bring Your Own Virtual Agent (BYOVA) gRPC endpoint while retaining the existing JWS/JWT validation.

## Selected section

## Before you begin

Prepare the following:

- A BYOVA gRPC endpoint that already performs JWS/JWT validation.
- A publicly issued certificate and corresponding private key for the domain of your gRPC server.
- The IdenTrust Commercial Root CA 1 certificate, available from the [IdenTrust Downloads and Drivers page](https://www.identrust.com/support/downloads), which your server uses to validate the Webex CCAI client certificate.
- The Webex CCAI certificate identity and FQDNs for your tenant's environment and region. Some Webex-provided fully qualified domain names (FQDNs) must be added to your allowlist. Obtain the exact values from the Webex Contact Center documentation provided for your tenant.

The certificate Subject values and required FQDNs vary by environment and region. Do not copy or infer values from another deployment.

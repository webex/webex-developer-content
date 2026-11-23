---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Before you begin

The customer organization must have the Media Forking offer (`MFCS`) on its Webex Contact Center subscription. The orderable SKUs are `A-FLEX-MEDSTRM` (Flex 3) and `E3CE-MEDSTRM` (Enterprise Agreement). For Flex 3 ordering details, see the [ordering guide](https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-og.html) and [data sheet](https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-ds.html).

Prepare a Webex Contact Center organization with a Full Admin who can authorize a Service App and an administrator who can edit, validate, and publish a flow. Implement a publicly reachable gRPC endpoint and secure it with TLS using a currently valid, publicly issued server certificate for the registered hostname. Optionally, add [mutual TLS (mTLS)](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/blob/main/mtls-authentication.md) for transport-level client authentication. Require a client certificate and validate its issuer, validity window, and tenant-documented Webex CCAI identity. Do not use mTLS instead of runtime JSON Web Signature (JWS) validation.

Use the [CiscoDevNet provider sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/media-forking) as a protocol reference, and adapt it to your processing and operational requirements. Its current Java validator retrieves keys before checking the issuer allowlist and tests every returned key; do not reuse that authentication path unchanged.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Register the data source
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Register the data source

Use the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources) with the organization-specific Service App access token.

1. Register the endpoint for the customer organization.
2. Follow the current API request schema. In `schemaId`, supply the Media Forking schema selected for the Service App; also supply the endpoint URL, audience, subject, nonce, and a supported token lifetime.
3. Confirm that the endpoint URL satisfies the Service App's data exchange domain rule.
4. Record the returned data source identifier.
5. Before the current JWS token expires, update the registered data source with the complete required payload, including its current `status` and a new `nonce`. The configured token lifetime can be at most 1440 minutes (24 hours). Renew with a safety margin before the signed JWT `exp`; do not wait until the last second shown by a REST expiry display. OAuth access-token renewal and data-source JWS renewal are separate operations; the sample does not automate them.

Use OAuth tokens only to manage the data source through the API. For each media RPC, extract the JWS from the gRPC `authorization` metadata and validate all of the following:

- The issuer against an allowlist of Webex issuers before retrieving verification keys.
- The `RS256` algorithm and RSA signature, using the Cisco public key identified by the JWS header's `kid` from `${iss}/oauth2/v2/keys/verificationjwk/`.
- The expiration time.
- The audience and subject claims against the values registered for the data source, and the presence of the JWT ID.
- The `com.cisco.datasource.url` claim against the registered endpoint URL.
- The `com.cisco.datasource.schema.uuid` claim against the selected Media Forking schema.
- The signed `com.cisco.org.uuid` claim against the opening metadata's `customer_org_id`. Keep that binding for later packets that omit the field, and reject an explicit mismatch.

Reject a missing or invalid JWS with `UNAUTHENTICATED`. Keep JWS validation enabled even when you use mTLS.

<a id="create-the-media-forking-configuration"></a>

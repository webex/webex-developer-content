---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-integration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the Integration in FedRAMP
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-integration). [Full Markdown](../../../../docs/create-a-fedramp-integration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Integrations, in contrast to bots, must be authorized by users and act on the user's behalf. During the authorization process the integration requests fine-grained controls which the authorizing user has visibility into. The rolls determine which REST endpoints the integration is allowed to call.

---

Just like bots, a Webex Integration must be created by a FedRAMP Webex Control Hub admin user in the applications file first. In the Webex FedRAMP environment, an integration can only be created via the Webex API. Once the integration is created, an OAuth client ID and secret can be used with an OAuth 2 authorization code flow to obtain an access token. The Integration creation by an admin is a one-time affair for each integration. Once the developer receives the OAuth URL and secret, they can handle user authorizations correctly.

## Selected section

## Using the Integration in FedRAMP

See the Requesting Permission section of the Integrations guide on the Webex for Developers site (<https://developer.webex.com/docs/integrations#requesting-permission>) for detailed instructions on how to use an integration.

Use <https://api-usgov.webex.com/v1/authorize> for the authorization URL and <https://api-usgov.webex.com/v1/access_token> for the access token URL.

Once your application is authorized by a full admin, a new access token and a refresh token are generated and can be used with the authorized Webex REST APIs. An access token is valid for 14 days and can be refreshed using the refresh token which is valid for 60 days. Creating a new access token refreshes the refresh token expiration timer.

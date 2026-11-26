---
type: Excerpt
canonical_url: https://developer.webex.com/docs/frequently-asked-questions
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Bots, Integrations, and Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/frequently-asked-questions). [Full Markdown](../../../../docs/frequently-asked-questions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

If you don't find the answer you're looking for here, please contact Webex Developer Support.

## Selected section

## Bots, Integrations, and Webhooks



> **Warning**
>
> Not supported for Webex for Government (FedRAMP)



### Do I need to submit my Bot to Webex App Hub for other people within my company to be able to use it?

No, a Bot does not need to be submitted to App Hub for it to be available to other Webex users in your organization. An App only needs to be submitted to App Hub if you want it listed on the [Webex App Hub](https://apphub.webex.com/) and available to any Webex user.

### Does a real user need to authorize an Integration, or can the authorization be completed programmatically?

A real user has to authorize with an integration through a web browser, there is no way to programmatically authorize with an integration. However, after you've gone through the OAuth flow once and have obtained your first access token and the refresh token, then the refresh token can be used to programmatically generate new access tokens.

### If I change the Scopes assigned to my Integration, will users need to reauthorize the Integration in order to invoke the newly added scope(s)?

Yes. They will need to go through the OAuth flow again in order to grant access to the integration for the newly added scopes.

### Can Apps (Bots, Integrations, Guest Issuers) be created through the API?

No. They can only be created in the [Developer Portal](https://developer.webex.com/my-apps).

### The employee who created our company's Bots has left the company. Will the Bots continue to function if their account is deactivated or deleted?

Yes.

### Is it possible to transfer a Bot that was created by one employee to the account of a different employee within our Org?

Yes. An org admin can do this using the [Application Transfer](https://applications.webexbots.cloud) app.
  
### What does `tokenlimit_reached` mean when trying to generate access tokens?
  
A Webex user is allowed to have up to 750 active tokens at a given time. If a user reaches that limit and tries to generate more tokens then a `tokenlimit_reached` error will be returned. A user can login to https://idbroker.webex.com/idb/profile#/ and end some of their sessions or have their Org admin revoke their tokens using the [Authorizations API](https://developer.webex.com/docs/api/v1/authorizations).

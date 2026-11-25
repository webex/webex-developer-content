---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Save the Service App Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/byods-node-js-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

The Webex Bring Your Own Data Service (BYoDS) Node.js SDK offers a simple way to set up and connect to your data sources when working with Webex services.

---

In this article, we’ll walk you through the steps to get it up and running quickly. For more in-depth details, we encourage you to explore the full documentation on specific features.

## Selected section

## Save the Service App Token

The `saveServiceAppRegistrationData` method uses the `org ID` and the service app's refresh token to retrieve the access token and store it in memory (since no `tokenStorageAdapter` is provided when creating the `BYODS` object):

```js
const orgId = 'your_org_id';
const refreshToken = 'service_app_refresh_token';

await sdk.tokenManager.saveServiceAppRegistrationData(orgId, refreshToken);
```

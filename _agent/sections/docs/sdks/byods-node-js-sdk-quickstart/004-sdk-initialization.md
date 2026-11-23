---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- SDK Initialization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/byods-node-js-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

The Webex Bring Your Own Data Service (BYoDS) Node.js SDK offers a simple way to set up and connect to your data sources when working with Webex services.

---

In this article, we’ll walk you through the steps to get it up and running quickly. For more in-depth details, we encourage you to explore the full documentation on specific features.

## Selected section

## SDK Initialization

Start by initializing the SDK with a few basic configuration settings:

```js
import { BYODS, LOGGER } from '@webex/byods';

const sdk = new BYODS({
  clientId: 'service_app_client_id',
  clientSecret: 'service_app_client_id',
  tokenStorageAdapter: undefined,
  logger: { level: LOGGER.INFO }
});
```



> **Info**
>
> For more information on `tokenStorageAdapter`, see [this document](https://developer.webex.com/docs/sdks/byods-nodejs-sdk-token-storage-adapter).

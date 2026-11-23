---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-nodejs-sdk-token-storage-adapter
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the Token Storage Adapter
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/byods-nodejs-sdk-token-storage-adapter). [Full Markdown](../../../../../docs/sdks/byods-nodejs-sdk-token-storage-adapter.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed introduction to the Token Storage Adapter in the BYoDS Node.js SDK, covering the implementation and usage of the `TokenStorageAdapter` class.

---

The `TokenStorageAdapter` is an interface that defines methods for storing, retrieving, and managing service app tokens. The `InMemoryTokenStorageAdapter` is the default implementation of this interface that stores tokens in memory.



> **Info**
>
> To learn more about service apps and tokens, see [Service Apps](https://developer.webex.com/docs/service-apps)

## Selected section

## Using the Token Storage Adapter

In order to leverage the `TokenStorageAdapter`, developers can extend the interface by creating their own custom adapter to connect to various databases or use the default `InMemoryTokenStorageAdapter`. 

Here's an example of how to create a custom token storage adapter:

```javascript
import { TokenStorageAdapter, OrgServiceAppAuthorization } from '@webex/byods';

class CustomTokenStorageAdapter implements TokenStorageAdapter {
  async setToken(orgId: string, token: OrgServiceAppAuthorization): Promise<void> {
    // Implement logic to store token in your database
  }

  async getToken(orgId: string): Promise<OrgServiceAppAuthorization | null> {
    // Implement logic to retrieve token from your database
  }

  async listTokens(): Promise<OrgServiceAppAuthorization[]> {
    // Implement logic to list all tokens from your database
  }

  async deleteToken(orgId: string): Promise<void> {
    // Implement logic to delete token from your database
  }

  async resetTokens(): Promise<void> {
    // Implement logic to reset all tokens in your database
  }
} 
```



> **Info**
>
> We strongly recommend you encrypt your tokens.



In order to use this custom `TokenStorageAdapter`, initialize the `BYODS` object:

```javascript
const customTokenStorageAdapter = new CustomTokenStorageAdapter();
const sdk = new BYODS({
  clientId: '<your-client-id>',
  clientSecret: '<your-client-secret>',
  tokenStorageAdapter: customTokenStorageAdapter,
});
```

To use the default `InMemoryTokenStorageAdapter`, simply pass `undefined` as the argument for the `tokenStorageAdapter`:

```javascript
const sdk = new BYODS({
  clientId: '<your-client-id>',
  clientSecret: '<your-client-secret>',
  tokenStorageAdapter: undefined,
});
```

For more information on creating the `BYODS` config, see [Quickstart Guide](https://developer.webex.com/docs/sdks/byods-nodejs-sdk-introduction).

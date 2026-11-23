---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-nodejs-sdk-token-storage-adapter
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- List All Tokens
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

## List All Tokens

To obtain a list of all stored tokens, use the `listTokens()` method:



| **Asynchronous** | **Parameters** | **Returns** |
| --- | --- | --- |
| Yes | No parameters required | `Promise<OrgServiceAppAuthorization[]>` |

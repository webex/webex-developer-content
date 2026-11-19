---
type: Guide
title: BYoDS Node.js SDK | Token Storage Adapter
display_title: Token Storage Adapter
canonical_url: https://developer.webex.com/docs/sdks/byods-nodejs-sdk-token-storage-adapter
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/byods-nodejs-sdk-token-storage-adapter)

This article provides a detailed introduction to the Token Storage Adapter in the BYoDS Node.js SDK, covering the implementation and usage of the `TokenStorageAdapter` class.

---

The `TokenStorageAdapter` is an interface that defines methods for storing, retrieving, and managing service app tokens. The `InMemoryTokenStorageAdapter` is the default implementation of this interface that stores tokens in memory.



> **Info**
>
> To learn more about service apps and tokens, see [Service Apps](https://developer.webex.com/docs/service-apps)



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

## Set a Token

You can set a token for a specific organization using the `setToken()` method:



| **Asynchronous** | **Parameters** | **Returns** |
| --- | --- | --- |
| Yes | `orgId` (string), `token` (OrgServiceAppAuthorization) | `Promise<void>` |

## Get a Token

To retrieve a token for a specific organization, use the `getToken()` method:



| **Asynchronous** | **Parameters** | **Returns** |
| --- | --- | --- |
| Yes | `orgId` (string) | `Promise<OrgServiceAppAuthorization>` |

## List All Tokens

To obtain a list of all stored tokens, use the `listTokens()` method:



| **Asynchronous** | **Parameters** | **Returns** |
| --- | --- | --- |
| Yes | No parameters required | `Promise<OrgServiceAppAuthorization[]>` |

## Delete a Token

To delete a token for a specific organization, use the `deleteToken()` method:



| **Asynchronous** | **Parameters** | **Returns** |
| --- | --- | --- |
| Yes | `orgId` (string) | `Promise<void>` |

## Reset All Tokens

To remove all tokens stored in the `InMemoryTokenStorageAdapter`, use the `resetTokens()` method:



| **Asynchronous** | **Parameters** | **Returns** |
| --- | --- | --- |
| Yes | No parameters required | `Promise<void>` |

## OrgServiceAppAuthorization Interface

This interface represents the authorization details for a service app within an organization. It includes the following properties:

```javascript
interface OrgServiceAppAuthorization {
  orgId: string;
  serviceAppToken: ServiceAppToken;
}
```

## ServiceAppToken Interface

This interface represents the token details for a service app. It includes the following properties:

```javascript
interface ServiceAppToken {
  accessToken: string;
  refreshToken: string;
  expiresAt: Date;
  refreshAccessTokenExpiresAt: Date;
}
```

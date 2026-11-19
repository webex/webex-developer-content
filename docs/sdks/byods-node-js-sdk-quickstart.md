---
type: Guide
title: BYoDS Node.js SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart)

The Webex Bring Your Own Data Service (BYoDS) Node.js SDK offers a simple way to set up and connect to your data sources when working with Webex services.

---

In this article, we’ll walk you through the steps to get it up and running quickly. For more in-depth details, we encourage you to explore the full documentation on specific features.

## Terminology



| Term                       | Description                                                                               |
| -------------------------- | ----------------------------------------------------------------------------------------- |
| DAS (Data Access Service)  | Part of Cisco’s internal system and communicates with `DAP` using the specified base URL. |
| DAP (Data Access Provider) | An external vendor data service designed for use with `DAS`.                              |
| Schema                     | The format or structure of the data to be stored in the `DAP`.                            |

## Prerequisites

Before continuing, make sure you meet the following prerequisites:

- Choose a schema from the [list of schemas](https://github.com/webex/dataSourceSchemas/) that fits your use case, and make a note of the `schema ID`, as you’ll need it later when working with the SDK.
- Configure a URL <https://abc.xyz.com/> for the `DAP` that is accessible by the `DAS`.
- Configure a [Service App](https://developer.webex.com/docs/service-apps) with the following configuration, approved by an organization admin. 
  - `Schema ID` - The ID of the schema to be used.
  - `Scopes` - The scopes should include `byods:datasource_read` and `byods:datasource_write`.
  - `Valid domains` - A list of valid domains where the `DAP` can be accessed.
  

> **Info**
>
> Save the `clientId` and `clientSecret` on hand, as you'll need them for SDK integration.


- An `Org ID` and the Service App’s `refresh` token.

## Installation

As this is a Node.js SDK, install the package in your application using either yarn or npm:

```bash
npm install @webex/byods
```

or

```bash
yarn add @webex/byods
```

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



## Save the Service App Token

The `saveServiceAppRegistrationData` method uses the `org ID` and the service app's refresh token to retrieve the access token and store it in memory (since no `tokenStorageAdapter` is provided when creating the `BYODS` object):

```js
const orgId = 'your_org_id';
const refreshToken = 'service_app_refresh_token';

await sdk.tokenManager.saveServiceAppRegistrationData(orgId, refreshToken);
```

## Data Source CRUD Operations

Before accessing the data source, obtain the client object:

```js
const orgId = 'your_org_id';

const client = sdk.getClientForOrg(orgId);
```

Now that you have the client object, you can now begin performing operations on the data sources.

### List all Registered Data Sources

To retrieve the list of all registered data sources:

```js
const response = await baseClient.dataSource.list();
const dataSources = response.data;

console.log('Data source list: ', dataSources);
```

### Create a Data Source

To create a data source, provide the required configuration parameters before calling the `create` method:

```js
const dataSourcePayload = {
  schemaId: 'schema_id',
  url: 'data_source_base_url',
  audience: 'developer app name',
  subject: 'purpose of the data source',
  nonce: 'a_random_string_for_token',
  tokenLifetimeMinutes: 'number_of_minutes'
};

const response = await baseClient.dataSource.create(dataSourcePayload);

console.log('Response: ', response.data);
```

### Update a Data Source

Update a data source by providing new configuration parameter values, similar to creating a new data source:

```js
const dataSourcePayload = {
  schemaId: 'schema_id',
  tokenLifetimeMinutes: 'number_of_minutes'
  url: 'data_source_base_url',
  subject: 'purpose of the data source',
  audience: 'developer app name',
  nonce: 'a_random_string_for_token',
  status: 'active', // or 'disabled'
  errorMessage: 'An error message associated with the data source',
};
const response = await baseClient.dataSource.update(id, dataSourcePayload);

console.log('Response: ', response.data);
```

### Delete a Data Source

Delete a data source by calling the `delete` method with the `data source ID`:

```js
const dataSourceId = 'data_source_id';
const response = await baseClient.dataSource.delete(dataSourceId);

console.log('Response: ', response.data);
```



> **Info**
>
> All CRUD operations are performed using the REST endpoints available at the provided base URL.



## JWS Token Verification

When the `DAS` sends a request to the `DAP`, it includes the `JWS` token in the header. To ensure the request is authentic and not from a malicious source, use the `sdk.verifyJWSToken(jws)` method for easy validation:

```js
const jws = 'a_jws_token';
const response = await sdk.verifyJWSToken(jws);

console.log('Response: ', response);
```

## Demo Server

Explore the SDK further by checking out this [Demo Server](https://github.com/webex/webex-js-sdk/tree/next/packages/byods-demo-server).

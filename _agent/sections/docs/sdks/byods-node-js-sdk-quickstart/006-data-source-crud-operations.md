---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Source CRUD Operations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/byods-node-js-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

The Webex Bring Your Own Data Service (BYoDS) Node.js SDK offers a simple way to set up and connect to your data sources when working with Webex services.

---

In this article, we’ll walk you through the steps to get it up and running quickly. For more in-depth details, we encourage you to explore the full documentation on specific features.

## Selected section

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

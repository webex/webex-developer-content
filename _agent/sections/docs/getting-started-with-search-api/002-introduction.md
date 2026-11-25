---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Introduction
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Introduction

A GraphQL API enables clients to construct queries to retrieve data. The queries are defined by the API server in the form of a GraphQL schema, which acts as a contract between the server and the client.

**Note:** For an introduction to GraphQL, refer: [GraphQL - 101](https://graphql.org/learn/)

The API allows access to the following:

1. Task related data stored as Customer Session Records (CSRs) and Customer Activity Records (CARs), accessible using the **taskDetails** graphql query.

2. Agent related data stored as Agent Session Records (ASRs) and Agent Activity Records (AARs), accessible using the **agentSession** graphql query.

3. Queue related data stored as Call Leg Records (CLRs), accessible using the **taskLegDetails** graphql query

Based on the operation, a query can be of two types:

1. **Query to fetch raw data:** fetching individual records stored, such as CSRs, ASRs, CARs, etc., with the ability to filter on data and apply pagination to get more records. In SQL terminology, this operation is analogous to

   `SELECT id, channelType FROM task WHERE channelType='telephony'`

   The structure of such a query is shown below

   ![Structure of query fetching raw data](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt86b18df865291ac4/69b1cffa507c8728a471d01c/Raw_query_sample_b6d475e5ae.png)

2. **Query to perform aggregations**: performing aggregation operations on record fields with support for group-bys, filtering, and pagination. In SQL terminology, the API is capable of the following queries:

   - `SELECT COUNT(id), MAX(totalDuration) FROM task`

   - `SELECT AVG(connectedDuration), AVG(totalDuration) FROM task  GROUP BY teamId, siteId`

   - `SELECT MAX(holdDuration) FROM task WHERE channelType='telephony' GROUP BY lastAgent.id`

   The structure of such a query can be found below

   ![Structure of a query performing aggregations](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltab85312b165ecabc/69b1cffafb62966ff0993c17/Aggregation_query_11ba02f950.png)

### Discover supported fields with Search Metadata

The Search Metadata API provides schema information for the Webex Contact Center Search GraphQL API, describing supported queries, fields, nested structures, data types, filters, sorting options, grouping capabilities, and aggregation operations.

Before constructing a Search GraphQL query, call [`GET /search/v2/meta`](https://developer.webex.com/docs/api/search-metadata/get-search-metadata) to retrieve the current field catalog. The endpoint requires a bearer token with the `cjp:config` or `cjp:config_read` scope and does not accept a request body.

The response's required `queries` array describes the supported query types and their fields. Use the response to:

- Identify root queries and nested objects by their GraphQL `type`.
- Traverse nested `fields` to find the field needed in a query.
- Check `filter`, `sortable`, and `groupBy` before using those capabilities.
- Check `aggregation.operations` for the aggregation operations supported by a field.

For example, before grouping an aggregation by a field, locate the field under the appropriate query and confirm that `groupBy` is `true`. Before applying an aggregation, use only an operation listed in `aggregation.operations`. This avoids constructing queries with unsupported fields or capabilities.

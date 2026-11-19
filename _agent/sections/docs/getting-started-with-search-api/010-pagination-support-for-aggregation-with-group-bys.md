---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Pagination Support
- Pagination Support for Aggregation with Group Bys
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Parent context

## Pagination Support

The `search` API supports pagination for both operations: performing aggregations and fetching raw data. The page size/ number of records returned by the query is fixed. Clients can fetch the next set of records using the `hasNextPage` and the `endCursor` fields in the response.

```graphql
{
  taskDetails(from: 1690964812000, to: 1691224012000) {
    tasks {
      id
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

`hasNextPage` is a boolean field that determines if more data exists for the given query. If the `hasNextPage` value is `true,` clients can fetch the value of the `endCursor` field, which is a string and acts as an identifier for the next page. `endCursor` value is passed in the subsequent query to fetch the next set of records.

The `pagination` argument accepts the `cursor` input parameter, which accepts the `endCursor` value and fetches the next page. A sample is given below.

```graphql
{
  taskDetails(
    from: 1690964812000
    to: 1691224012000
    pagination: { cursor: "<VALUE-OF-endCursor-FROM-PREVIOUS-QUERY" }
  ) {
    tasks {
      id
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

The page size of a query depends on the query type and the operations, these are given below.

| Operation         | Query Type     | Page Size | Total number of Records that can be fetched with pagination |
| ----------------- | -------------- | --------- | ------------------------------------------------------------ |
| Fetch raw data    | taskDetails    | 250       | 100000                                                       |
| Fetch raw data    | agentSession   | 250       | No Limit                                                     |
| Fetch raw data    | taskLegDetails | 500       | 100000                                                       |
| Aggregation query | taskDetails    | 1000      | No Limit                                                     |
| Aggregation query | agentSession   | 1000      | No Limit                                                     |
| Aggregation query | taskLegDetails | 1000      | No Limit                                                     |

**Note:** In order to fetch the first page, the `pagination` argument can either be omitted or the `cursor` value can be set to **NA**.

Sample queries demonstrating pagination when fetching raw data are given below.

| Usecase                                              | Query Type/ Record   | Query                                                                                                                                                                                                | Response                                                                                                                                                                                                      |
| ---------------------------------------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch the first page of records with ASR attributes. | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Pagination%20.graphql>)                         | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Pagination%20-response.json>)                            |
| Fetch the next page of data.                         | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Pagination%202.graphql>)                        | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Pagination%202-response.json>)                           |
| Fetch the next & the last page.                      | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Pagination%203.graphql>)                        | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Pagination%203-response.json>)                           |
| Fetch the first page of records with CSR attributes  | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Pagination%20query.graphql>)     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskDetails%2FSamples%20for%20Raw%20Data%20Fetching%2FPagination%20query%20-response.json>) |
| Fetch the next page of data                          | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Pagination%20query%202.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Pagination%20query%202-response.json>)    |
| Fetch the next & the last page                       | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Pagination%20query%203.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Pagination%20query%203-response.json>)    |
| Fetch the first page of records with CLR attributes  | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Pagination.graphql>)                          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Pagination%20-response.json>)                          |
| Fetch the next page of data                          | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Pagination%202.graphql>)                      | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Pagination%202%20-%20response.json>)                   |

## Selected section

### Pagination Support for Aggregation with Group Bys

In case of aggregation queries involving group bys, pagination can be done to fetch more records. Sample queries are given below.

| Usecase                                                                                                                                                                     | Query Type/ Record   | Query                                                                                                                                                                                                                 | Response                                                                                                                                                                                                                          |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Get the number of contacts handled on a daily basis per agent, team, site, queue & entrypoint for each channel.                                                             | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20pagination%20query.graphql>)                    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20pagination%20query%20-response.json>)                       |
| Get the next page of records for the above query.                                                                                                                           | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20pagination%20query%202.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20pagination%20query%202-response.json>)                      |
| Get the count of "connected" or "ctq-accepted" activities on a daily basis per agent, team, site, queue & entrypoint                                                        | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithPaginationForCAR.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithPaginationForCAR-response.json>)                      |
| Get the next page of records for the above query.                                                                                                                           | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithPaginationForCAR2.graphql>)               | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithPaginationForCAR2.json>)                              |
| Fetch the total connected count, average connectedDuration,total idleCount, average idleDuration.                                                                           | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20Pagination.graphql>)                           | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20Pagination%20-response.json>)                              |
| Get the next page of records for the above query.                                                                                                                           | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20Pagination%202.graphql>)                       | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20Pagination%202-response.json>)                             |
| Find the max duration for each agent,team,site and state.                                                                                                                   | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationPaginationQueryForAAR.graphql>)                   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationPaginationQueryForAAR-response.json>)                         |
| Get the next page of records for the above query.                                                                                                                           | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationPaginationQueryForAAR2.graphql>)                  | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationPaginationQueryForAAR2-response.json>)                        |
| Get average of queue duration, ringing duration, connected duration and self-service duration on a daily basis per agent, team, site, queue & entrypoint for each channel.  | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Group%20by%20Aggregation%20with%20Pagination.graphql>)     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Group%20by%20Aggregation%20with%20Pagination%20-%20response.json>)     |
| Get the next page for the above query.                                                                                                                                      | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Group%20by%20Aggregation%20with%20Pagination%202.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Group%20by%20Aggregation%20with%20Pagination%202%20-%20response.json>) |

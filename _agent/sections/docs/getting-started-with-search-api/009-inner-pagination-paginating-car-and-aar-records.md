---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Pagination Support
- Inner Pagination / Paginating CAR and AAR records
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

### Inner Pagination / Paginating CAR and AAR records

Both CAR and AAR records are exposed within the `activities.nodes` field, which provides a list of records. To fetch more CAR and AAR records, inner pagination can be used; this enables pagination within the records instead of paginating the records themselves.

To fetch more records within `activities.nodes` , the cursor can be retrieved from the `activities.pageInfo` field, which contains the `endCursor` and `hasNextPage` fields. This cursor value can be passed into the `after` argument.

The `activities` field supports the following two arguments to support inner pagination

1. _first_ - Accepts an Int value which determines the number of records to be fetched. By default, the value is set to **25** and the maximum supported value is **100**.

2. _after_ - Accepts a String value which determines the next page to be fetched.

**Note:** The total count of records can be read using the `activities.totalCount` field.

**Note:** Since inner pagination enables record level pagination, the cursor value retrieved from a record is not applicable for other records, hence it is highly recommended to use a `filter` to exclude the other records.

A sample query to fetch next **5** CAR records for task id **329fe2ed-adc6-489a-ba2c-7cf74cf284b4** after the cursor value of **djF8MTB8bDoxMzoxNzY4NTQyNTk1NjA4fHM6NTc6MzI5ZmUyZWQtYWRjNi00ODlhLWJhMmMtN2NmNzRjZjI4NGI0LTE3Njg1NDI1OTU2MDgtd3JhcHVw** is shown below

```graphql
{
  taskDetails(
    from: 1768471320000
    to: 1770026539000
    filter: { id: { equals: "329fe2ed-adc6-489a-ba2c-7cf74cf284b4" } }
  ) {
    tasks {
      id
      activities(
        first: 5
        after: "djF8MTB8bDoxMzoxNzY4NTQyNTk1NjA4fHM6NTc6MzI5ZmUyZWQtYWRjNi00ODlhLWJhMmMtN2NmNzRjZjI4NGI0LTE3Njg1NDI1OTU2MDgtd3JhcHVw"
      ) {
        totalCount
        nodes {
          id
          eventName
        }
        pageInfo {
          hasNextPage
          endCursor
        }
      }
    }
  }
}
```

Sample queries for inner pagination of CAR and AAR are given below.

| Usecase                                                           | Query / Record Type | Query                                                                                                                                                                                         | Response                                                                                                                                                                                            |
| ----------------------------------------------------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| For a task fetch the next 2 CAR records after a given cursor      | taskDetails / CAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/innerPagination.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/innerPagination-response.json>) |
| For a channelId fetch the next 3 AAR records after a given cursor | agentSession / AAR  | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/innerPagination.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/innerPagination-response.json>)                |

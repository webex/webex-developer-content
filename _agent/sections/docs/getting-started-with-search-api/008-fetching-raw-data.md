---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Fetching Raw Data
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Fetching Raw Data

Fields from individual records can also be fetched; this is referred to as fetching raw data. Any query without the `aggregations` argument is treated as a query to fetch raw data.

Based on the fields that are requested and the filter criteria specified in the query, the API will read data from the appropriate type of record and return the requested field for each record. **It is recommended to fetch fields belonging to the same type of record**. Refer to the data dictionary section for more details.

Sample taskDetails query to fetch _id_ field in a taskDetails query.

```graphql
{
  taskDetails(from: 1644859375000, to: 1671038575000) {
    tasks {
      id
    }
  }
}
```

**Note:** When fetching AAR and CAR data, the query span i.e. `from` and `to` cannot exceed more than 30 days

Samples for various data types are given below

| Usecase                                                                                                                                                                                                                                                                  | Query / Record Type  | Query                                                                                                                                                                                                 | Response                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch isActive, id, createdTime, endedTime, totalDuration, lastAgent.id, queueCount and queueDuration attributes for tasks with pagination information.                                                                                                                  | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Simple%20query.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Simple%20query-response.json>)          |
| Fetch id, channelType of task and the number of CARs, eventName, duration of CARs, along with pagination information                                                                                                                                                     | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/SimpleQueryForCARFields.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/SimpleQueryForCARFields-response.json>) |
| Fetch the agentSessionId, agentId, teamId, siteId, agentSession startTime, endTime, isActive and channelInfo fields such as channelId, channelType and few metrics along with pagination information.                                                                    | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Simple%20query.graphql>)                         | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Simple%20query-response.json>)                         |
| Fetch the agentSession Id, agent Id, team Id, site Id, agentSession's startTime, endTime, isActive and channel level details such as channelId, channelType. For each channel also includes the AAR with id, startTime, endtime, state fields and pagination information | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/SimpleQueryForAARFields.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/SimpleQueryForAARFields-response.json>)                |
| Fetch id of the taskLeg, taskId, createdTime, queue id, entrypoint id, number of successful consults, consult duration and pagination information                                                                                                                        | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Simple%20Query.graphql>)                       | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Simple%20Query-response.json>)                       |

### Filtering data

To fetch data matching a filter criteria, the `filter` and `extFilter` arguments can be used. Refer [section on filtering](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for details

### Sorting Support

When fetching raw data, the data can be sorted in ascending or descending order. Fields supporting sorting accept a `sort` argument where the sorting criteria can be specified as
`asc` for ascending and `desc` for descending. The below sample sorts data in ascending order of "createdTime" field.

```graphql
{
  taskDetails(from: 1644859375000, to: 1671038575000) {
    tasks {
      id
      createdTime(sort: asc)
    }
  }
}
```

Refer to the [data dictionary](https://developer.webex.com/docs/getting-started-with-search-api#data-dictionary) for fields supporting sorting.
Sample queries to fetch data with sorting are given below.

| Usecase                                                                                                                                                                 | Query Type/ Record   | Query                                                                                                                                                                                                                    | Response                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Fetch id, createdTime and endedTime for tasks sorted based on ascending order of createdTime field                                                                      | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Sorting%20results%20based%20on%20a%20field.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Sorting%20results%20based%20on%20a%20field-response.json>) |
| For a specific task, fetch id, channelType and count of activities, also fetch the id and created time for each activity sorted based on ascending order of createdTime | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/SortingQueryForCAR.graphql>)                         | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/SortingQueryForCAR.json>)                                  |
| Fetch id of the taskLeg, taskId, channelType and createdTime based on ascending order of createdTime field                                                              | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Sorting%20samples%20based%20on%20a%20field.graphql>)              | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Sorting%20samples%20based%20on%20a%20field-response.json>)              |

### Pagination support for fetching raw data

Pagination is supported for raw queries, Refer [section on pagination](https://developer.webex.com/docs/getting-started-with-search-api#pagination-support-1) for details

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Performing Aggregations
- Support for filtering within Aggregation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Parent context

## Performing Aggregations

Any query with the `aggregations` argument is treated as an aggregation query; this argument accepts a list of objects.

Each object requires the following mandatory arguments :

1. _field_ - String, denotes the identifier or field name on which the aggregation needs to be done.
2. _name_ - String, identifier to determine the result of the aggregation operation.
3. _type_ - Enum, defines the aggregation operation; depending on the data type of the field specified, the following aggregations are supported.

| Type        | Description                                                     | Supported data types             |
| ----------- |-----------------------------------------------------------------| -------------------------------- |
| count       | Counts the occurrence of the field across documents.             | Int, Long, Float, String boolean |
| min         | Returns the minimum value of the field across documents.        | Int, Long, Float                 |
| max         | Returns the maximum value of the field across documents         | Int, Long, Float                 |
| sum         | Aggregates the value of the field across documents.             | Int, Long, Float                 |
| average     | Returns the average of the field across documents.              | Int, Long, Float                 |
| cardinality | Returns the count of unique value of the field across documents | Int, Long, Float, String boolean |

The following arguments are optional :

1. _filter_ - Denotes the filter criteria for documents for the particular aggregation.

2. _predicate_ - Applicable only for global variables, Refer to the [Global Variable section ](https://developer.webex.com/docs/getting-started-with-search-api#performing-aggregations-on-global-variables)for more details.

Refer below for the syntax of `aggregations` argument.

```graphql
aggregations: [
  {
     field: "totalDuration"
     type: max
     name: "maxDurationTelephony"
  }
]
```

Sample queries to perform aggregations on various data types are given below.

| Usecase                                                                            | Query Type/ Record   | Query                                                                                                                                                                                     | Response                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch the count of tasks and their average totalDuration                           | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20query.graphql>)     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20query%20-response.json>)    |
| Fetch number of unique queues tasks were queued into.                             | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryForCAR.graphql>)  | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryForCAR-response.json>)    |
| Fetch total connectedCount and average of connectedDuration across agent sessions. | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20query.graphql>)    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20query-response.json>)      |
| Fetch count of unique ids and max duration of activities across sessions.          | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationQueryForAAR.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationQueryForAAR-response.json>)   |
| Fetch average queue duration and average ringing duration across taskLegs          | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20query.graphql>)  | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20query%20-response.json>) |

## Selected section

### Support for filtering within Aggregation

In an aggregation query, filters can be applied for all the aggregations or for individual aggregations, which are referred to as global filters and sub-filters respectively.

When filtering has to be applied to all aggregations, the top-level `filter` and extFilter arguments can be used. Refer to the [Filtering section](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for more details on the syntax and usage. Refer to the below general syntax for global filtering support.

```graphql
filter : {
    lastTeam : {
        name : {equals : "team1"}
    }
},
aggregations: [
    {
        field: "id"
        type: count
        name: "count of ids"
    },
    {
        field: "totalDuration"
        type: average
        name: "average of totalDuration"
    }
]
```

Sample queries to perform aggregations with filter criteria on various data types are given below.

| Usecase                                                                                                    | Query Type/ Record     | Query                                                                                                                                                                                                             | Response                                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Get the number of tasks handled and their average total duration of tasks handled by the particular queue. | taskDetails / CSR      | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20query%20with%20filters.graphql>)            | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20query%20with%20filters-response.json>)            |
| Fetch the average duration of parked events for _telephony_ contacts.                                      | taskDetails / CAR      | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithFiltersForCAR.graphql>)               | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithFiltersForCAR-response.json>)               |
| Fetch the count of agents and teams for active sessions.                                                   | agentSession / ASR     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20global%20filter%20query.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20global%20filter%20query-response.json>)          |
| For a given agent, fetch the count of connected events across sessions.                                    | agentSession / AAR     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationQueryWithGlobalFilterForAAR.graphql>)         | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationQueryWithGlobalFilterForAAR-response.json>)         |
| Get the count of abandoned callLegs                                                                        | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20query%20with%20Global%20Filter.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20query%20with%20Global%20Filter-response.json>) |

#### Aggregations with sub filters

Filtering can also be done for individual aggregation using the `filter` and `extfilter` argument in the aggregation object. Refer below general syntax for sub-filter support

```graphql
aggregations: [
  {
     field: "totalDuration"
     type: max
     name: "maxDurationTelephony"
     filter: { channelType: { equals: telephony } }
  }
]
```

Sample queries to perform aggregations with sub-filter criteria on various data types are given below.

| Usecase                                                                                                                        | Query Type/ Record    | Query                                                                                                                                                                                                        | Response                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------ | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Fetch the number of tasks handled by multiple queues.                                                                          | taskDetails / CSR     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20query%20with%20sub-filters.graphql>)   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Aggregation%20query%20with%20sub-filters-response.json>)   |
| Fetch the average duration customers are put on hold by specific agents                                                        | taskDetails / CAR     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithSubFiltersForCAR.graphql>)       | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/AggregationQueryWithSubFiltersForCAR-response.json>)       |
| Fetch the count of agents where 1)'channelType' is 'telephony' 2) 'channelType' is 'social' 3)idle agents 4) connected agents. | agentSession / ASR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20sub-filter%20query.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Aggregation%20sub-filter%20query-response.json>)          |
| Find the count of connected and ringing events.                                                                                | agentSession / AAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationQueryWithSubFilterForAAR.graphql>)       | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/AggregationQueryWithSubFilterForAAR-response.json>)       |
| Fetch the number of calls queued into specific queues.                                                                         | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20query%20with%20sub-filter.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20query%20with%20sub-filter-response.json>) |

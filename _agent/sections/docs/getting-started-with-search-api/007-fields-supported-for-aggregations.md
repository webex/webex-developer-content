---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Performing Aggregations
- Fields supported for aggregations
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

### Fields supported for aggregations

Refer [data dictionary](https://developer.webex.com/docs/getting-started-with-search-api#data-dictionary) for fields supporting aggregation.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Performing Aggregations
- Performing group by operation
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

### Performing group by operation

To perform a group by operation, the fields required for group bys should be included in the requested fields. The below sample performs a group by on the **lastAgent.id** field.

```graphql
{
  taskDetails(
    from: 1617401436000
    to: 1619647836000
    aggregations: [
      {
        field: "totalDuration"
        type: max
        name: "maxDurationTelephony"
        filter: { channelType: { equals: telephony } }
      }
    ]
  ) {
    tasks {
      lastAgent {
        id # Group by on lastAgent.id
      }
      aggregation {
        name
        value
      }
    }
  }
}
```

Some sample queries to perform group by on various data types.

| Usecase                                                                                                                         | Query Type / Record  | Query                                                                                                                                                                                                     | Response                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| For each queue, fetch the number of contacts that were handled and its average queue duration.                                  | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Group%20by%20aggregation%20query.graphql>)        | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Group%20by%20aggregation%20query-response.json>)           |
| For each site, agent and channelType, get the number of tasks handled and the average value of connected duration.              | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Group%20by%20multiple%20fields.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Group%20by%20multiple%20fields%20-response.json>)          |
| For each queue the tasks are queued into, get the average duration of parked activity.                                          | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/GroupBySingleFieldsForCAR.graphql>)               | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/GroupBySingleFieldsForCAR-response.json>)                  |
| For each agent and queue, count the number of times the call was presented.                                                     | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/GroupByMultipleFieldsForCAR.graphql>)             | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/GroupByMultipleFieldsForCAR-response.json>)                |
| For each channel type, find the total connected count, average connected duration, total idle count, and average idle duration. | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Group%20by%20query.graphql>)                     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Group%20by%20query-response.json>)                        |
| For each team, site and channel type, compute the total connected count, average connected duration, and average idle duration. | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Group%20by%20multiple%20fields%20query.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Group%20by%20multiple%20fields%20query%20-response.json>) |
| Find the maximum duration of each agent activity.                                                                               | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/GroupBySingleFieldsQueryForAAR.graphql>)         | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/GroupBySingleFieldsQueryForAAR-response.json>)            |
| For each agent and activity state find the max of duration.                                                                     | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/GroupByMultipleFieldsQueryForAAR.graphql>)       | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/GroupByMultipleFieldsQueryForAAR-response.json>)          |
| Get count of consults, average queued duration and ringing duration for each queue                                              | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20with%20group%20bys.graphql>)     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Aggregation%20with%20group%20bys-response.json>)        |
| Calculate the number of consult-transfers and blind-transfers done into the queue and entrypoint.                               | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Group%20bys%20multiple%20fields.graphql>)      | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Group%20bys%20multiple%20fields%20-response.json>)      |

#### Interval based group bys.

Aggregations can be grouped based on time intervals such as `DAILY` , `WEEKLY` etc. by adding the `intervalStartTime` as a requested field and using the `aggregationInterval` argument, which accepts two parameters.

- _interval_ - Mandatory argument: accepts an Enum, Based on the query span (i.e. difference of the values passed in `from` and `to`) the following values are supported.

| Query Span        |                            Supported intervals                             |
| :---------------- | :------------------------------------------------------------------------: |
| <= DAY            | `FIFTEEN_MINUTES`,`THIRTY_MINUTES`, `HOURLY`, `DAILY`, `WEEKLY`, `MONTHLY` |
| > DAY & <= 7 DAYS |          `THIRTY_MINUTES`, `HOURLY`, `DAILY`, `WEEKLY`, `MONTHLY`          |
| > 7 DAYS          |                        `DAILY`, `WEEKLY`, `MONTHLY`                        |

- timezone - Optional argument: accepts a String representing the timezone, using which the intervals should be formed; the default timezone used is `UTC`.

Refer the below sample syntax for the `aggregationInterval` argument.

```graphql
aggregationInterval : {
    interval : DAILY
    timezone : "America/New_York"
}
```

Sample queries to perform interval based aggregations.

| Usecase                                                                                                                                | Query Type/ Record   | Query                                                                                                                                                                                                                           | Response                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Get the number of tasks handled on a daily basis (based on Asia/Kolkata) for each channelType and site                                 | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Interval%20based%20timezone%20supported%20aggregation%20query.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/Interval%20based%20timezone%20supported%20aggregation%20query-response.json>) |
| Find the average duration of parked events on a daily basis for each queue.                                                            | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/IntervalBasedTimezoneSupportedAggregationQueryForCAR.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Performing%20Aggregations/IntervalBasedTimezoneSupportedAggregationQueryForCAR-response.json>)          |
| Fetch the total connected Count, average connected duration, total idle count, average of idleDuration on a daily basis for each team. | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Interval%20timezone%20based%20aggregation%20query.graphql>)            | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/Interval%20timezone%20based%20aggregation%20query-response.json>)            |
| Fetch max ringing duration on daily basis.                                                                                             | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/IntervalTimezoneBasedAggregationQueryForAAR.graphql>)                  | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Performing%20Aggregations/IntervalTimezoneBasedAggregationQueryForAAR-response.json>)                  |
| For each queue get the number of calls queued and number of consults into the queue on a daily basis (based on Asia/Kolkata)           | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Interval%20timezone%20based%20aggregation%20query.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Performing%20Aggregations/Interval%20timezone%20based%20aggregation%20query%20-%20response.json>)    |

**Note:** The number of fields used for a group by operation in an aggregation query cannot exceed 10.

#### Pagination support

When using group bys, the data can be paginated to get more results, using the `pagination` argument. Refer to the [Pagination section](https://developer.webex.com/docs/getting-started-with-search-api#pagination-support-1) for more details.

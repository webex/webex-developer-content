---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Query Definitions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Query Definitions

The following sections describe the query types supported in detail.

### TaskDetails Query

A taskDetails query operates over **CSR** and **CAR** records.

#### Sample Query

A sample query to fetch tasks created on 1st January 2023

```graphql
{
  taskDetails(
    from: 1672531200000 # 1st January 2023 00:00:00 UTC
    to: 1672617599000 # 1st January 2023 23:59:59 UTC
  ) {
    tasks {
      id # Scalar field
      isActive
      channelType
      createdTime
      endedTime
      lastAgent {
        # Object / Composite field
        id # Scalar field
      }
    }
  }
}
```

**Note:** Scalar fields are atomic and represent indivisible values, these are basic data types like Int, Long, String, Boolean, Float. Object fields are defined by the graphQL schema and contain other fields within them.Refer GraphQL documentation for [Scalar types](https://graphql.org/learn/schema/#scalar-types), [type system and objects](https://graphql.org/learn/schema/#object-types-and-fields)

#### GraphQL Schema

The GraphQL schema structure is defined as given below.

```graphql
taskDetails(
    from: Long!  # MANDATORY ARGUMENT
    to: Long!    # MANDATORY ARGUMENT
    timeComparator: QueryTimeType
    case_insensitive: Boolean
    filter: TaskDetailsFilters
    extFilter: TaskDetailsSpecificFilters
    aggregations: [TaskV2Aggregation]
    aggregationInterval: IntervalData
    pagination: Pagination
): TaskDetailsList
```

#### Arguments

1. _from_ - Mandatory argument: accepts a _Long_ value representing the epoch timestamp, which defines the start of the query span. By default, the `createdTime` field is used for comparison, but this can be overridden to use `endedTime` by using the `timeComparator` argument.

2. _to_ - Mandatory argument: accepts a _Long_ value representing the epoch timestamp, which defines the end of the query span. By default, the `createdTime` field is used for comparison, but this can be overridden to use `endedTime` by using the `timeComparator` argument.

3. _timeComparator_ - Optional argument: accepts a value of the `QueryTimeType` type. This defines the field which `from` and `to` arguments use for retrieving documents. Accepted values are `createdTime` and `endedTime`.

4. _case_insensitive_ - Optional argument: accepts a Boolean value. When set to true, equals and not equals filters for supported string fields become case-insensitive. Supported fields: `customer.name`, `customer.email`, `lastQueue.name`, `lastSite.name`, `lastTeam.name`, `lastEntryPoint.name`, `previousQueue.name`, `firstQueueName`, `lastAgent.name`, `previousAgentName`, `preferredAgentName`, `campaignName`.

5. _filter_ - Optional argument: accepts a _TaskDetailsFilters_ object. This is used to filter results based on a criteria defined on CSR fields. Refer to the [filtering section](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for more details.

6. _extFilter_ - Optional argument: accepts a _TaskDetailsSpecificFilters_ object. This is used to filter results based on a criteria defined on CAR fields. Refer to the [filtering section](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for more details.

7. _aggregations_ - Optional argument: accepts a List of `TaskV2Aggregation`. This is used to perform aggregations over data. Refer to the [aggregations section](https://developer.webex.com/docs/getting-started-with-search-api#performing-aggregations) for more details.

8. _aggregationInterval_- Optional argument: accepts an `IntervalData` object. This is used when time-based aggregation needs to be performed. Refer to the [aggregations section](https://developer.webex.com/docs/getting-started-with-search-api#interval-based-group-bys) for more details.

9. _pagination_ - Optional argument: accepts an object of `Pagination` object. This is used to perform pagination. Refer to the [pagination section](https://developer.webex.com/docs/getting-started-with-search-api#pagination-support-1) for more details.

Some sample queries can be found below

| Usecase                                                                                                                                                 | Query / Record Type | Query                                                                                                                                                                                                 | Response                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch isActive, id, createdTime, endedTime, totalDuration, lastAgent.id, queueCount and queueDuration attributes for tasks with pagination information. | CSR                 | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Simple%20query.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Simple%20query-response.json>)          |
| Fetch id, channelType of task and the number of CARs, eventName, duration of CARs, along with pagination information                                    | CAR                 | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/SimpleQueryForCARFields.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/SimpleQueryForCARFields-response.json>) |

### AgentSession Query

An agentSession query operates over **ASR** and **AAR** records.

#### Sample Query

A sample query to fetch agentSessions created on 1st January 2023.

```graphql
{
  agentSession(
    from: 1672531200000 # 1st January 2023 00:00:00 UTC
    to: 1672617599000 # 1st January 2023 23:59:59 UTC
  ) {
    agentSessions {
      agentId # Scalar field
      teamId
      siteId
      startTime
      endTime
      channelInfo {
        # Object / Composite field
        channelId
        channelType # Scalar field
        totalDuration
        connectedDuration
      }
    }
  }
}
```

#### GraphQL schema

The GraphQL schema structure is defined as given below.

```graphql
agentSession(
    from: Long! # MANDATORY ARGUMENT
    to: Long!   # MANDATORY ARGUMENT
    filter: AgentSessionFilters
    extFilter: AgentSessionSpecificFilters
    aggregations: [AgentSessionV2Aggregation]
    aggregationInterval: IntervalData
    pagination: Pagination
): AgentSessions
```

#### Arguments

1. _from_ - Mandatory argument: accepts a _Long_ value representing epoch timestamp which defines the start of the query span, the `startTime` field is used for comparison.

2. _to_ - Mandatory argument: accepts a _Long_ value representing the epoch timestamp, which defines the end of the query span; the `startTime` field is used for comparison.

3. _filter_ - Optional argument: accepts an _AgentSessionFilters_ object. This is used to filter results based on user-defined criteria on ASR fields. Refer to the [filtering section](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for more details.

4. _extFilter_ - Optional argument: accepts an _AgentSessionSpecificFilters_ object. This is used to filter results based on user-defined criteria on AAR fields. Refer to the [filtering section](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for more details.

5. _aggregations_ - Optional argument: accepts a List of `AgentSessionV2Aggregation`, This is used to perform aggregations over data. Refer to the [aggregations section](https://developer.webex.com/docs/getting-started-with-search-api#performing-aggregations) for more details.

6. _aggregationInterval_- Optional argument: accepts an `IntervalData` object. This is used when time-based aggregation needs to be performed. Refer to the [aggregations section](https://developer.webex.com/docs/getting-started-with-search-api#interval-based-group-bys) for more details.

7. _pagination_ - Optional argument: accepts an object of `Pagination` object. This is used to perform pagination. Refer to the [pagination section](https://developer.webex.com/docs/getting-started-with-search-api#pagination-support-1) for more details.

Sample query to fetch ASR fields can be found [here](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Simple%20query.graphql>), the response for the same is [here](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Simple%20query-response.json>).

| Usecase                                                                                                                            | Query / Record Type | Query                                                                                                                                                                                  | Response                                                                                                                                                                                     |
| ---------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch the agentSession details, agent details, team details, site details and channel details along with pagination information.   | ASR                 | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Simple%20query.graphql>)          | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Simple%20query-response.json>)          |
| Fetch the agentSession , agent details, team details, site details and channel details. For each channel also includes AAR details | AAR                 | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/SimpleQueryForAARFields.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/SimpleQueryForAARFields-response.json>) |

### TaskLegDetails Query

An `taskLegDetails` query operates over CLR data.

**Note:** The `TaskLegDetails` object is a part of Queue Based Reporting Early Access, and will only return data if you are a member of the Early Access Program.

#### Sample Query

A sample query to fetch taskLegs for a particular task on 1st January 2023

```graphql
{
  taskLegDetails(
    from: 1672531200000 # 1st January 2023 00:00:00 UTC
    to: 1672617599000 # 1st January 2023 23:59:59 UTC
    filter: { taskId: { equals: "2d6ef583-4a57-40ec-83b4-390d14625e19" } }
  ) {
    taskLegs {
      id
      taskId
      queue {
        name
      }
      handleType
    }
  }
}
```

#### GraphQL schema

The GraphQL schema structure is defined as

```graphql
taskLegDetails(
    from: Long! # MANDATORY ARGUMENT
    to: Long!   # MANDATORY ARGUMENT
    timeComparator: QueryTimeType
    filter: TaskLegDetailsFilters
    aggregations: [TaskLegV2Aggregation]
    aggregationInterval: IntervalData
    pagination: Pagination
): TaskLegDetailsList
```

#### Arguments

1. _from_ - Mandatory argument: accepts a _Long_ value representing the epoch timestamp which defines the start of the query span, By default, the `createdTime` field is used for comparison, but this can be overridden to use `endedTime` by using the `timeComparator` argument.

2. _to_ - Mandatory argument: accepts a _Long_ value representing epoch timestamp which defines the end of the query span, By default, the `createdTime` field is used for comparison, but this can be overridden to use `endedTime` by using the `timeComparator` argument.

3. _timeComparator_ - Optional argument: accepts a value of `QueryTimeType` type. This defines the field  which `from` and `to` arguments use for retrieving documents. Accepted values are `createdTime` and `endedTime`.

4. _filter_ - Optional argument: accepts an _TaskLegDetailsFilters_ object. This is used to filter results based on user-defined criteria. Refer to the [filtering section](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for more details.

5. _aggregations_ - Optional argument: accepts a List of TaskLegV2Aggregation. This is used to perform aggregations over data. Refer to the [aggregations section](https://developer.webex.com/docs/getting-started-with-search-api#performing-aggregations) for more details.

6. _aggregationInterval_- Optional argument: accepts an `IntervalData` object. This is used when time-based aggregation needs to be performed. Refer to the [aggregations section](https://developer.webex.com/docs/getting-started-with-search-api#interval-based-group-bys) for more details.

7. _pagination_ - Optional argument: accepts an object of `Pagination` object. This is used to perform pagination. Refer to the [pagination section](https://developer.webex.com/docs/getting-started-with-search-api#pagination-support-1) for more details.

| Usecase                                                                                                                                             | Query / Record Type | Query                                                                                                                                                                           | Response                                                                                                                                                                              |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch id of the taskLeg, taskId, createdTime, queue id, entrypoint id, number of successful consults, consult duration and pagination information. | CLR                 | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Simple%20Query.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Simple%20Query-response.json>) |

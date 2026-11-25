---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Support for Filtering data
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Support for Filtering data

Filtering of data is supported using the `filter` and `extFilter` arguments. Filtering is supported in both operations, fetching raw data or performing aggregations; the syntax for defining the filter criteria remains the same.

The distinction between `filter` and `extFilter` is the type of fields they allow filtering on. In a _taskDetails_ query, `filter` is used for filtering data based on fields available in a CSR record, and `extFilter` is used for filtering data based on fields available in a CAR record. Similarly, in an _agentSession_ query, `filter` is used for filtering based on ASR fields and `extFilter` is used for filtering based on AAR fields. In a _taskLegDetails_ query, `extfilter` is **not** supported and `filter` can be used to filter data based on CLR fields.

The general formula or syntax for filtering is

```graphql
filter : {
    fieldName : { operator : value }
}
```

### Filtering based on Scalar fields

Based on the data type different filter operators are available

#### String Operators for filtering

The following operators are supported for _String_ fields

| Operator  | Description                                       |
| --------- | ------------------------------------------------- |
| equals    | Checks if two values are equal.                   |
| notequals | Checks if two values are not equal.               |
| match     | Checks if a value matches a specified pattern.    |
| contains  | Checks if a string contains a specific substring. |

Given below is a sample for filtering using _equals_ operator, _equals_ can be replaced with _notequals_.

```graphql
filter: {
    origin: { equals: "+12344565678" }
}
```

_match_ operator can be used filter based on a regex/pattern.

```graphql
filter: {
    origin: { match: "+12345678.+" }
}
```

_contains_ operator to filter on a substring match of a string field

```graphql
filter: {
    campaignName : { contains : "Sales"}
}
```

#### Numerical Operators for filtering

The following operators are supported for numerical fields

| Operator  | Description                     |
| --------- | ------------------------------- |
| equals    | Exact match operation           |
| notequals | Negate operation                |
| gt        | Greater than operation          |
| gte       | Greater than or equal operation |
| lt        | Less than operation             |
| lte       | Less than or equal operation    |

Using the compound operator `and` and numerical operators we can build range filter as given in below sample.

```graphql
filter: {
    and: [
        { totalDuration: { lte: 120000 } }
        { totalDuration: { gte: 60000 } }
    ]
}
```

| Usecase                                                                                                           | Query / Record Type  | Query                                                                                                                                                                                               | Response                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch _telephony_ tasks which are marked *abandoned*.                                                             | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/binaryFilterOperators.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/binaryFilterOperators-response.json>) |
| Fetch records for active sessions where channelType is not _telephony_ and teamName exists.                       | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/binaryFilterOperation.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/binaryFilterOperation-response.json>)                |
| Fetch id of taskLeg, created time, queue id, agent/owner id, entrypoint id and ended time for a particular task. | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Simple%20Filtering.graphql>)                 | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Simple%20Filtering-response.json>)                 |

#### Compound operators for filtering

Compound filters include 2 operators - `and` & `or` operator, these accept multiple filter criterion in the form of a list.

Fetch records where channelType is telephony and status is either created or ended

```graphql
    filter: {
      and: [
        { channelType: { equals: telephony } }
        {
          or: [
            { status: { equals: "ended" } }
            { status: { equals: "created" } }
          ]
        }
      ]
    }
```

Some sample queries using compound operators are given below.

| Usecase                                                                         | Query Type/ Record   | Query                                                                                                                                                                                                                  | Response                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch _telephony_ tasks where totalDuration is between 30s and 60s.             | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Filtering%20using%20compound%20operators.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Filtering%20using%20compound%20operators-response.json>) |
| Fetch records where agent session is active and channelType is _telephony_.     | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Filtering%20using%20compound%20operators.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Filtering%20using%20compound%20operators-response.json>)                |
| Fetch id of taskLegs, queue ids and owner ids associated with a specific queue. | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Filtering%20using%20compound%20operators.graphql>)              | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Filtering%20using%20compound%20operators-response.json>)              |

### Filtering based on Composite objects

Filtering is only supported for scalar fields and not for objects; however, scalar fields inside objects can be filtered.

Consider a scenario where filtering is performed on the `subject` field within the `email` object, which is nested inside the top-level `channelMetaData` field. The structure of the query reflects this hierarchy, starting from the top-level field and traversing through subfields until reaching the leaf field.

```graphql
filter: {
    channelMetaData: {
        email: { subject: { equals: "sample subject" } }
    }
}
```

Since all the CAR and AAR fields are present in the `activities` object, filtering using `extFilter` also follows the same pattern, one such sample is given below

```graphql
extFilter : {
    activities : {
        nodes : {
            queueId : {equals : "40162355-72f4-4dc1-b710-2f8c94e5d14b"}
        }
    }
}
```

Some samples for filtering on object types are given below

| Usecase                                                                 | Query Type/ Record   | Query                                                                                                                                                                                                         | Response                                                                                                                                                                                                            |
| ----------------------------------------------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch tasks which are handled by a specific team.                       | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Filtering%20on%20object%20types.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Filtering%20on%20object%20types-response.json>) |
| For a single interaction fetch the queues the contact is _parked_ into. | taskDetails / CAR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Filtering%20using%20extFilters.graphql>)  | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Samples%20for%20Raw%20Data%20Fetching/Filtering%20using%20extFilters-response.json>)  |
| Fetch ASR records where channelType is _telephony_.                     | agentSession / ASR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Filtering%20on%20object%20types.graphql>)                | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/Filtering%20on%20object%20types-response.json>)                |
| Fetch AAR records where activity _state_ is _connected_.                | agentSession / AAR   | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/FitleringOnextFilter.graphql>)                           | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/agentSession/Raw%20Data%20Fetching/FilteringOnextFilter-response.json>)                           |
| Fetch taskLegs associated with a specific queue and agents.             | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Filtering%20on%20object%20types.graphql>)              | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Fetching%20Raw%20Data/Filtering%20on%20object%20types-response.json>)              |

### Fields supported for filtering

Refer [data dictionary](https://developer.webex.com/docs/getting-started-with-search-api#data-dictionary) for fields supporting filtering.

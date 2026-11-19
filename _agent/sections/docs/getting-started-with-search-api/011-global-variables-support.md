---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Global Variables Support
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Global Variables Support

[Global variables](https://help.webex.com/en-us/article/ngfdsbi/Manage-global-variables) are exposed as part of the TaskDetails and TaskLegDetails queries. Depending on the data type of the variable, the following 5 types of global variables are stored and can be fetched:

1. stringGlobalVariables

2. booleanGlobalVariables

3. integerGlobalVariables

4. doubleGlobalVariables

5. longGlobalVariables

To fetch the global variable data, pass the name of the global in the argument
Eg: To get data of the Global Variable of String Type with name as GlobalVariable1

```graphql
# 'name' argument is mandatory.
#  This block will fetch name and value for the stringGlobalVariable named 'GlobalVariable1'
stringGlobalVariables(name: "GlobalVariable1") {
    name
    value
}
```

Multiple global variables of the same type can be fetched using [aliasing](https://graphql.org/learn/queries/#aliases):

```graphql
# To fetch multiple global variables use aliasing - https://graphql.org/learn/queries/#aliases
GV1: stringGlobalVariables(name: "GV1") {
    name
    value
}
GV59: stringGlobalVariables(name: "GV59") {
    name
    value
}
```

Some sample queries on globalVariables for taskDetails and taskLegDetails

| Usecase                                                      | Query / Record Type  | Query                                                                                                                                                                                       | Response                                                                                                                                                                                          |
| ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch value of integer, string and boolean global variables. | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Fetching%20global%20variables.graphql>)    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Fetching%20global%20variables-response.json>)    |
| Fetch value of integer, string and boolean global variables. | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Fetching%20global%20variables.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Fetching%20global%20variables-response.json>) |

### Filtering based on global variables

Filtering on global variables is supported by passing the global variable name in the `name` argument and values to be filtered in the `value` argument.
Eg: Fetch the records Global Variable (GV1) of string with value ABC123

```graphql
{
    stringGlobalVariables: {
        name: { equals: "GV1" }
        value: { equals: "ABC123" }
    }
}
```

Eg: Fetch the records Global Variable (GV2) of integer type greater than 100

```graphql
{
    integerGlobalVariables: {
        name: { equals: "GV2" }
        value: { gt: 100 }
    }
}
```

Refer [section on filtering](https://developer.webex.com/docs/getting-started-with-search-api#support-for-filtering-data) for different operators supported.

Some sample queries on global variables with filtering for taskDetails and taskLegDetails

| Usecase                                                                      | Query / Record Type  | Query                                                                                                                                                                                                     | Response                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Filter tasks based on a condition on string and integer global variables.    | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Filter%20based%20on%20global%20variables.graphql>)       | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Filter%20based%20on%20global%20variables-response.json>)       |
| Filter taskLegs based on a condition on string and integer global variables. | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Filtering%20based%20on%20global%20variables.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Filtering%20based%20on%20global%20variables-response.json>) |

### Performing Aggregations on global variables

For performing aggregation on global variables we need to use the `predicate` argument in the `aggregations` object
Eg: Sum of all values of integer global variable named `GV2` .

```graphql
 {
    field: "integerGlobalVariables.value"
    name: "Sum of GV2"
    type: sum
    # Predicate is used to define which global variable needs to be considered for the operation.
    predicate: { integerGlobalVariables: { name: { equals: "GV2" } } }
}
```

Eg: Fetch unique value of a string global variable named `GV1`.

```graphql
 {
    field: "stringGlobalVariables.value"
    name: "Unique of GV1"
    type: cardinality
    # Predicate is used to define which global variable needs to be considered for the operation.
    predicate: { stringGlobalVariables: { name: { equals: "GV1" } } }
}
```

Refer [section on aggregation](https://developer.webex.com/docs/getting-started-with-search-api#performing-aggregations) for more details on aggregation types.

Some sample aggregations on globalVariables for taskDetails and taskLegDetails

| Usecase                                                          | Query / Record Type  | Query                                                                                                                                                                                               | Response                                                                                                                                                                                                  |
| ---------------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Calculate sum of integer global variable named "GV2" across CSRs | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Aggregation%20on%20global%20variables.graphql>)    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Aggregation%20on%20global%20variables-response.json>)    |
| Calculate sum of integer global variable named "GV2" across CLRs | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Aggregation%20on%20global%20variables.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Aggregation%20on%20global%20variables-response.json>) |

### Performing group by operation on global variables

For performing group by's using global variables, the fields required for group bys should be included in the requested fields, The sample below performs a group by operation on the value of a string global variable named `Global_Language`.

```graphql
{
  # Group by using  Global Variables
  # To perform a group by on a global variable add the global variable in the selection set.
  taskDetails(
    from: 1655449155512
    to: 1671038575000
    aggregations: [
      { field: "id", name: "count of calls", type: count }
      {
        field: "integerGlobalVariables.value"
        name: "Sum of GV2"
        type: sum
        predicate: { integerGlobalVariables: { name: { equals: "GV2" } } }
      }
    ]
  ) {
    tasks {
      # Group by on stringGlobalVariable named "Global_Language".
      stringGlobalVariables(name: "Global_Language") {
        value
      }
      aggregation {
        name
        value
      }
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

Using aliasing group by can be done on multiple global variables of the same type.

```graphql
{
  # Group by using  Global Variables
  # To perform a group by on a global variable add the global variable in the selection set.
  taskDetails(
    from: 1655449155512
    to: 1671038575000
    aggregations: [
      { field: "id", name: "count of calls", type: count }
      {
        field: "integerGlobalVariables.value"
        name: "Sum of GV2"
        type: sum
        predicate: { integerGlobalVariables: { name: { equals: "GV2" } } }
      }
    ]
  ) {
    tasks {
      # Group by on stringGlobalVariable named "Global_Language".
      stringGlobalVariables(name: "Global_Language") {
        value
      }
      # Group by on stringGlobalVariable named "Location".
      Location: stringGlobalVariables(name: "Location") {
        value
      }
      aggregation {
        name
        value
      }
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

Some sample group by's on globalVariables with aggregations for taskDetails and taskLegDetails

| Query Type                                                                                                                               | Query / Record Type  | Query                                                                                                                                                                                               | Response                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fetch count of calls and sum of integer global variable named "GV2", per unique value of string global variable named "Global_Language". | taskDetails / CSR    | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Group%20by%20on%20global%20variables.graphql>)     | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskDetails/Global%20Variables/Group%20by%20on%20global%20variables-response.json>)            |
| Fetch count of calls and sum of integer global variable named "GV2", per unique value of string global variable named "Global_Language". | taskLegDetails / CLR | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Aggregation%20on%20global%20variables.graphql>) | [link](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/taskLegDetails/Global%20Variables/Group%20by%20based%20on%20global%20variables-response.json>) |

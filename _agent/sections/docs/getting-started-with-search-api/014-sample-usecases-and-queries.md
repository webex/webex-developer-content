---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Sample Usecases and queries
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Sample Usecases and queries

This repository is organized into multiple files that you can paste directly into the section of the interactive editor on **[Webex Developer Portal - Search Tasks](https://developer.webex.com/docs/api/v1/search/search)**

| #   | File Name                                                                                                                                                                                        | Comments                                                                                                                                                                 | Query Type              |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------- |
| 1   | [simple.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/simple.graphql>)                                     | SIMPLE: Simply retrieve all task IDs.                                                                                                                                    | Fetching raw data       |
| 2   | [basicFields.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/basicFields.graphql>)                           | BASIC: Basic query to request for certain fields.                                                                                                                        | Fetching raw data       |
| 3   | [advanced.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/advanced.graphql>)                                 | AGGREGATES/FORMULAS: Usage of filters, aggregates, pagination and custom fields.                                                                                         | Performing Aggregations |
| 4   | [callback.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/callbackFilter.graphql>)                           | FILTER: Get the Task details using CallBack filters and logical operators to match a condition.                                                                          | Fetching raw data       |
| 5   | [realTimeQueuedTasks.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/realTimeQueuedTasks.graphql>)           | FILTER: Fetch Real-time (Active) Queued Tasks on the System - using filters.                                                                                             | Fetching raw data       |
| 6   | [lastAgentInteraction.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/lastAgentInteraction.graphql>)         | LAST AGENT INTERACTIONS: Usage of filters, aggregates, pagination and custom fields to find when the customer called last in a 7 day window and who they reached.        | Performing Aggregations |
| 7   | [interactionDetails.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/interactionDetails.graphql>)             | INTERACTION DETAILS: Usage of filters, aggregates, pagination and custom fields to find out information about a specific interaction using INTERACTION ID/TaskID/CSR ID. | Performing Aggregations |
| 8   | [totalCallsByAni.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/totalCallsByAni.graphql>)                   | Filter with Aggregates: Usage of filters with aggregations, for total calls made by a specific customer.                                                                 | Performing Aggregations |
| 9   | [globalVariables.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/globalVariables.graphql>)                   | GLOBAL VARIABLES: Usage of the Global Variables field to extract a specific global variable or a combination of two global variables.                                    | Fetching raw data       |
| 10  | [globalVariableFilter.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/globalVariableFilter.graphql>)         | GLOBAL VARIABLES: Usage of the Global Variables as a FILTER to extract a specific tasks for a specific global variable.                                                  | Fetching raw data       |
| 11  | [allContactFields.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/allContactFields.graphql>)                 | ALL FIELDS: Extracting all fields from the Contact Session Record = Task Details.                                                                                        | Fetching raw data       |
| 12  | [allAgentSessionFields.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/allAgentSessionFields.graphql>)       | ALL FIELDS: Extracting all fields from the Agent Session Record = ASR Details.                                                                                             | Fetching raw data       |
| 13  | [FetchAgentSkill.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/FetchAgentSkill.graphql>)                   | SKILLS : Extracting Agent skills from an ASR record                                                                                                                      | Fetching raw data       |
| 14  | [FilteringUsingAgentSkill.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/FilteringUsingAgentSkill.graphql>) | SKILLS : Filtering ASR records based on Agent skill criteria                                                                                                             | Fetching raw data       |
| 15  | [GroupByAgentSkills.graphql](<https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample/More%20Examples/GroupByAgentSkills.graphql>)             | SKILLS: Group ASR records based on set of skills                                                                                                                         | Performing Aggregations |

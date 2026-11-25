---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommendations and best practices
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md) [Restrictions](012-restrictions.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Recommendations and best practices

- While querying data or performing aggregations, it is recommended to use fields belonging to only a single data type. Ex: In a taskDetails query, it is recommended to use fields either from CSR or from CAR and not from both. Similarly, for AgentSession query, it is recommended to use fields either from ASR or from AAR.

- It is recommended to use the _taskDetails_ query for any Task related data instead of the older _task_ query.

- For aggregations, use the _aggregations_ argument; the older argument _aggregation_ supports limited functionalities and is not recommended to be used.

- Performing group by's on global variables and skill-related fields is not recommended as the performance may be impacted based on the volume of data.

- Performing group by's on Int, Double or numerical fields or String fields that have a high number of unique values is not recommended.

- It is recommended to pass a `TrackingId` header with a valid UUID in the request payload, For example - `007bfe3b-a257-4caa-9882-fbd710cc671e`;this allows for easier debugging by support teams in case of any issue.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-started-with-search-api
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Restrictions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-started-with-search-api). [Full Markdown](../../../../docs/getting-started-with-search-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Watch Getting Started With the Search API](001-watch-getting-started-with-the-search-api.md)

## Article introduction

Learn all about the Webex Contact Center search GraphQL API in this article.

---

For a quick overview of the `search` API and how to use our documentation, refer the video below:

## Selected section

## Restrictions

1. For any type of query, the query span, i.e. the `from` and `to,` should not exceed a period of 12 months.

2. When fetching AAR and CAR raw data, the query span, i.e. `from` and `to` cannot exceed more than 30 days.

3. When fetching CSR and CLR documents using pagination, the API supports up to a maximum of 100K records.

4. The number of fields used for a group by operation in an aggregation query cannot exceed 10.

5. When using `extFilter` in a query to fetch raw data, if matching records for first page cannot be populated from the first 2500 Records (based on query span and `filter` criteria), then the API will respond back with 413 Status code.

6. The total number of arguments allowed across filters, extFilter and predicates is capped at a default limit of 1000.

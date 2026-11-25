---
type: Excerpt
canonical_url: https://developer.webex.com/docs/rest-api-basics
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Pagination
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/rest-api-basics). [Full Markdown](../../../../docs/rest-api-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes the basics of consuming a REST API - namely the Webex API, as well as how to use Postman to explore a REST API.

## Selected section

## Pagination

As adoption of Webex continues to grow, so does the amount of content being shared by team members. We've addressed this in the Webex APIs by including support for pagination.

It would be impractical to return all messages in a busy space, for example. With pagination, the Webex API returns a specific number of items at a time; allowing your app to request more items as needed.

### Navigating Pages

The Webex APIs implement the [RFC5988 (Web Linking)](http://tools.ietf.org/html/rfc5988) standard for pagination. When requesting a list of resources the response may contain a `Link` header containing the URLs to the first, next, and previous page.

For example, requesting `GET /people?displayName=Harold` may return a link header like this one:

```http
Link: <https://webexapis.com/v1/people?displayName=Harold&max=10&before&after=Y2lzY29zcGFyazovL3VzL1BFT1BMRS83MTZlOWQxYy1jYTQ0LTRmZWQtOGZjYS05ZGY0YjRmNDE3ZjU>; rel="next"
```

Notice the `rel="next"` at the end of the line. This tells your app that another page is available and provides the URL to fetch it.

The list of possible relationship types are:



| Relationship | Description               |
| ------------- | --------------------------- |
| `next`        | Link to the next page       |
| `first`       | Link back to the first page |
| `prev`        | Link to the previous page   |

Please note that only the `rel="next"` link header is guaranteed at this time. We may include other link types, that are defined in the RFC5988 (Web Linking) standard, in the future.

### Controlling Page Size

When requesting a list of resources the `max` query parameter may be used to control the number of items returned per page. For example, requesting `GET /people?displayName=Harold&max=2` tells the API to return only 2 items per page.

If the requested `max` query parameter value exceeds what a particular API endpoint allows, only the maximum number of items allowed per page for that endpoint will be returned. A `rel="next"` link header will be present if another page of results is available.

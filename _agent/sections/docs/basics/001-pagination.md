---
type: Excerpt
canonical_url: https://developer.webex.com/docs/basics
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Pagination
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/basics). [Full Markdown](../../../../docs/basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While working with the Webex REST API is easy, there are a few things we standardize on throughout the API, such as pagination of long result sets or HTTP response codes.

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

**Note:** Because data is loaded dynamically, a `Link` header may sometimes point to an empty page if all data was already returned on the previous page. In some APIs (such as `GET /membership?personEmail=`), you may encounter empty pages with `Link` headers still present, as memberships not visible to the requester's organization are filtered out. As a best practice, continue paginating through all pages until no `next` link header is present, collecting data from each page along the way.

### Controlling Page Size

When requesting a list of resources the `max` query parameter may be used to control the number of items returned per page. For example, requesting `GET /people?displayName=Harold&max=2` tells the API to return only 2 items per page.

If the requested `max` query parameter value exceeds what a particular API endpoint allows, only the maximum number of items allowed per page for that endpoint will be returned. A `rel="next"` link header will be present if another page of results is available.

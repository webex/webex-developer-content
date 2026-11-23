---
type: Excerpt
canonical_url: https://developer.webex.com/docs/common-api-errors
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Error Response Body
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/common-api-errors). [Full Markdown](../../../../docs/common-api-errors.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Invalid Authorization header (400)](001-invalid-authorization-header-400.md)

## Article introduction

Our APIs return standard HTTP status codes for request responses. If an error occurs, more information will be provided in the response.

## Selected section

## Error Response Body

If an API request returns with an error, the error response (with CORS headers) will follow this format:

```json
{
    "error": {
        "key": 400,
        "message": [
            {
                "description": "Invalid Authorization header, must contain: Bearer <token_string>"
            }
        ]
    },
    "trackingId": "AUTHSVC_fed07d0a-044a-4dae-bbe8-0ee0ece260f5"
}
```

### Tracking ID

When contacting support for questions or debugging a specific request, please include the Tracking ID ("`.trackingId` in error response) so we can easily find the request logs.

---
type: Guide
title: Common API Errors
display_title: Common API Errors
canonical_url: https://developer.webex.com/docs/common-api-errors
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/common-api-errors)

Our APIs return standard HTTP status codes for request responses. If an error occurs, more information will be provided in the response.

## Invalid Authorization header (400)

All API requests require an 'Authorization' header, containing a Bearer token. The value of this header must be of the form `Bearer <token string>`.  Else, the request will not be processed, and you will get a 400 response. See [Authentication](https://developer.webex.com/docs/authentication) for how to get a token.

## Invalid Access Token (401)

The token provided in Authorization header must be valid (unaltered) and unexpired.  Else, you will get `401 Unauthorized` response and the request will not be processed. See [Authentication](https://developer.webex.com/docs/authentication) for how to get a token.

## Operation is Forbidden (403)

All API requests require a variety of scopes. In order to interact with a given API, a user's token needs to have the correct scope, or else they will be forbidden from interacting with the API.

Additionally, some APIs require the user to have an administrator role.

## Too Many Requests (429)

Too many requests have been sent in a given amount of time so the request has been rate limited. The request has a valid token and has not been processed. The 429 response will have proper CORS headers, but will not have a body.

See [Rate Limiting](https://developer.webex.com/docs/rate-limiting) for details.

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

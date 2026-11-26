---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-authentication
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Send the personal access token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-authentication). [Full Markdown](../../../../docs/webex-connect-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use a Webex personal access token to authenticate requests to the digital asset APIs for Email and Chat assets. Chat assets support Push Notifications, Live Chat, and In-App Messaging.

## Selected section

## Send the personal access token

Include the token in each request to a digital asset API using the bearer scheme:

```http
Authorization: Bearer <personal-access-token>
```

Do not send the token as a query parameter or in the request body.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-authentication
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Identify the organization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-authentication). [Full Markdown](../../../../docs/webex-connect-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use a Webex personal access token to authenticate requests to the digital asset APIs for Email and Chat assets. Chat assets support Push Notifications, Live Chat, and In-App Messaging.

## Selected section

## Identify the organization

Include the organization ID in the `x-organization-id` header. The organization must be associated with the user represented by the token.

```http
x-organization-id: <organization-id>
```

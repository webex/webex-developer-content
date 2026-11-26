---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-authentication
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- How access is evaluated
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-authentication). [Full Markdown](../../../../docs/webex-connect-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use a Webex personal access token to authenticate requests to the digital asset APIs for Email and Chat assets. Chat assets support Push Notifications, Live Chat, and In-App Messaging.

## Selected section

## How access is evaluated

Authentication verifies the token and identifies the Webex user. Authorization then verifies that:

- The token contains the scope required for the digital asset operation.
- The user can access the organization identified by `x-organization-id`.
- The user has permission to manage the requested asset.

The required token scope permits the API operation; it does not grant organization access or a higher administrative role.

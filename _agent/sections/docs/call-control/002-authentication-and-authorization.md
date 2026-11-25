---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication and Authorization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Authentication and Authorization

### Service Apps

The Service App concept is how third-party applications can be authorized to perform admin-level call control actions on behalf of an organization.

A Service App declares the scopes it requires. An organization administrator can associate a Service App with its organization, granting it the access specified in the Service App's scopes.

Once granted access, a third-party application can retrieve an access token associated to that Service App. The access token authorizes the third-party application to perform API calls based on its authorized scopes.

For more information about Service Apps, see the [Using Webex Service Apps](https://developer.webex.com/docs/service-apps) guide.

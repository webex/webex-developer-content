---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- What's Possible with Admin APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin). [Full Markdown](../../../../docs/admin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](003-authentication.md)

## Article introduction

Manage Webex users, licenses, and hybrid services programmatically with the Webex Admin APIs.

## Selected section

## What's Possible with Admin APIs

The Webex APIs include several APIs that allow administrators to programmatically perform administrative actions such as provisioning a user or assigning a license to a user. By automating administration, user management and provisioning can be performed from an existing tool, rather than using the [Webex Control Hub](https://admin.webex.com).

Using these APIs, an admin can, for example:

- [Create a user](https://developer.webex.com/docs/api/v1/people/create-a-person)
- [Update a user](https://developer.webex.com/docs/api/v1/people/update-a-person)
- [View license usage of an organization](https://developer.webex.com/docs/api/v1/licenses/get-license-details)
- [View available roles of an organization](https://developer.webex.com/docs/api/v1/roles/list-roles)
- [Manage Hybrid Services licenses and users](https://developer.webex.com/docs/managing-hybrid-services-licenses)
- [View information about Hybrid Clusters](https://developer.webex.com/docs/api/v1/hybrid-clusters) or [Hybrid Connectors](https://developer.webex.com/docs/api/v1/hybrid-connectors)



> **Warning**
>
> If your organization uses the [Cisco Directory Connector](https://www.cisco.com/go/hybrid-services-directory) to synchronize Webex user accounts with Active Directory accounts, then you cannot _create_ or _delete_ Webex users using the [People API](https://developer.webex.com/docs/api/v1/people). Additionally, the People API will not allow you to _update_ any attributes of your existing users that are being synchronized by the Directory Connector.

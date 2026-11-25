---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin). [Full Markdown](../../../../docs/admin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Manage Webex users, licenses, and hybrid services programmatically with the Webex Admin APIs.

## Selected section

## Authentication

Use of these APIs requires you to be an administrator of an organization. If you are not an administrator of an organization, but wish to develop against these APIs, see below for instructions on how to get administrator access to an Administration Sandbox organization.

If you are an administrator, log into this site to get a development auth token with the necessary scopes.

To create an [Integration](https://developer.webex.com/create/docs/integrations) that will act on behalf of an administrator, include one or more of the following scopes when requesting an auth token via OAuth:



The scope catalog for category `admin` is generated dynamically. View the [official portal page](<https://developer.webex.com/docs/admin>) for scope names and descriptions.

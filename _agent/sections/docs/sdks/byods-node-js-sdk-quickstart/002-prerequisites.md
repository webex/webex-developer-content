---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/byods-node-js-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/byods-node-js-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex Bring Your Own Data Service (BYoDS) Node.js SDK offers a simple way to set up and connect to your data sources when working with Webex services.

---

In this article, we’ll walk you through the steps to get it up and running quickly. For more in-depth details, we encourage you to explore the full documentation on specific features.

## Selected section

## Prerequisites

Before continuing, make sure you meet the following prerequisites:

- Choose a schema from the [list of schemas](https://github.com/webex/dataSourceSchemas/) that fits your use case, and make a note of the `schema ID`, as you’ll need it later when working with the SDK.
- Configure a URL <https://abc.xyz.com/> for the `DAP` that is accessible by the `DAS`.
- Configure a [Service App](https://developer.webex.com/docs/service-apps) with the following configuration, approved by an organization admin. 
  - `Schema ID` - The ID of the schema to be used.
  - `Scopes` - The scopes should include `byods:datasource_read` and `byods:datasource_write`.
  - `Valid domains` - A list of valid domains where the `DAP` can be accessed.
  

> **Info**
>
> Save the `clientId` and `clientSecret` on hand, as you'll need them for SDK integration.


- An `Org ID` and the Service App’s `refresh` token.

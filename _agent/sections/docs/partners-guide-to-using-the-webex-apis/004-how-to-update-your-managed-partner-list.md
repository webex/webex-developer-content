---
type: Excerpt
canonical_url: https://developer.webex.com/docs/partners-guide-to-using-the-webex-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- How to Update Your Managed Partner List
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/partners-guide-to-using-the-webex-apis). [Full Markdown](../../../../docs/partners-guide-to-using-the-webex-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations and Best Practices](005-limitations-and-best-practices.md)

## Article introduction

Our partner community who utilizes Webex APIs will find this guide extremely helpful. If you're a reseller partner who manages customers and users, or an ISV partner that incorporates our app frameworks into your services, there's something for you here.

## Selected section

## How to Update Your Managed Partner List

As a partner admin, you have multiple ways to update your managed organizations list. You can directly log in to the customer's Control Hub (admin.webex.com), or you can rely on certain API endpoints that dynamically update your list. For more control, you can use the GET /organizations/{id} command. If the {id} belongs to a managed organization, your partner admin account will be updated but only for the next 24 hours.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/partners-guide-to-using-the-webex-apis
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Navigating the Managed Partner List
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/partners-guide-to-using-the-webex-apis). [Full Markdown](../../../../docs/partners-guide-to-using-the-webex-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations and Best Practices](005-limitations-and-best-practices.md)

## Article introduction

Our partner community who utilizes Webex APIs will find this guide extremely helpful. If you're a reseller partner who manages customers and users, or an ISV partner that incorporates our app frameworks into your services, there's something for you here.

## Selected section

## Navigating the Managed Partner List

Each partner admin has a list of managed organizations linked to their account. When you invoke an API on a managed customer organization, the system checks if you have the necessary rights to act on that organization. If your managed customer list is not up to date you likely will receive a 403 http status code and you will need to update your managed partner list.

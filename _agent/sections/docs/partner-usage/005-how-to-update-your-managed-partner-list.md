---
type: Excerpt
canonical_url: https://developer.webex.com/docs/partner-usage
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- How to Update Your Managed Partner List
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/partner-usage). [Full Markdown](../../../../docs/partner-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations and Best Practices](006-limitations-and-best-practices.md)

## Article introduction

This page serves as partner specific "hints" guide for the general Webex APIs

## Selected section

## How to Update Your Managed Partner List

As a partner admin, you have multiple ways to update your managed organizations list. You can directly log in to the customer's Control Hub (admin.webex.com), or you can rely on certain API endpoints that dynamically update your list. For more control, you can use the GET /organizations/{id} command. If the {id} belongs to a managed organization, your partner admin account will be updated but only for the next 24 hours.

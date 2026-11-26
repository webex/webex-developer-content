---
type: Excerpt
canonical_url: https://developer.webex.com/docs/partner-usage
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Navigating the Managed Partner List
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/partner-usage). [Full Markdown](../../../../docs/partner-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations and Best Practices](006-limitations-and-best-practices.md)

## Article introduction

This page serves as partner specific "hints" guide for the general Webex APIs

## Selected section

## Navigating the Managed Partner List

Each partner admin has a list of managed organizations linked to their account. When you invoke an API on a managed customer organization, the system checks if you have the necessary rights to act on that organization. If your managed customer list is not up to date you likely will receive a 403 http status code and you will need to update your managed partner list.

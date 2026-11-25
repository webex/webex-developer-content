---
type: Excerpt
canonical_url: https://developer.webex.com/docs/fedramp-overview
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- FedRAMP application types
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/fedramp-overview). [Full Markdown](../../../../docs/fedramp-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex FedRAMP environment is separate and distinct from our “commercial” environment and is tailored to the Federal government's collaboration business. Access to the Webex FedRAMP environment is for federal government organizations and partners invited by those entities.

## Selected section

## FedRAMP application types

In the Webex commercial environment, a set of application types is available that do not translate directly to the FedRAMP environment. There are Bots (standalone persons), Integrations (acting on a user's behalf), Embedded Apps,  Service Apps, and Guest Issuers (creation of anonymous persons) available in the commercial environment. Guest Issuers are unavailable in FedRAMP, and no substitute is currently planned. Those app types have been intentionally disabled. As such, this document will cover the development of Bots, Integrations and Embedded Apps as its primary goal.

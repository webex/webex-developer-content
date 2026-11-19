---
type: Excerpt
canonical_url: https://developer.webex.com/docs/fedramp-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- FedRAMP API URL and Control Hub URL
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/fedramp-overview). [Full Markdown](../../../../docs/fedramp-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex FedRAMP environment is separate and distinct from our “commercial” environment and is tailored to the Federal government's collaboration business. Access to the Webex FedRAMP environment is for federal government organizations and partners invited by those entities.

## Selected section

## FedRAMP API URL and Control Hub URL

The Webex APIs in FedRAMP are accessible under api-usgov.webex.com. For example, the message endpoint’s address would be https://api-usgov.webex.com/v1/messages, which is notably distinct from the commercial environment at webexapis.com. Applications for the FedRAMP environment must call that API address alone. The Control Hub login screen is available at [https://admin-usgov.webex.com](https://admin-usgov.webex.com), also separate and distinct from the commercial environment.

The Webex XML APIs used to control the meeting experience are accessed under the site name like the commercial APIs. For example, if one of FedRAMP customer site's name is ‘ABC,’ its DNS is abc.webex.com, and the XML API can be accessed at https://abc.webex.com/WBXService/XMLService.

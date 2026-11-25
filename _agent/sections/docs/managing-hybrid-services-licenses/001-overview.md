---
type: Excerpt
canonical_url: https://developer.webex.com/docs/managing-hybrid-services-licenses
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/managing-hybrid-services-licenses). [Full Markdown](../../../../docs/managing-hybrid-services-licenses.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex API includes several methods which can be used by administrators to programmatically manage license usage of Webex Hybrid Services.

## Selected section

## Overview

The following Hybrid Services licenses can be managed via the Webex API:

- Hybrid Call Aware
- Hybrid Call Connect
- Hybrid Exchange Calendar
- Hybrid Google Calendar

### Requirements

- API users must be assigned the “Full Administrator” role for their organization to access license information and display information about all people within the organization.
- API users must be assigned the “Full Administrator” role or have the `spark-admin:people_write` scope enabled to add licenses to users.

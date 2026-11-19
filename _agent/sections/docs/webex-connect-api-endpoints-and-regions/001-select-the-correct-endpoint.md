---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Select the correct endpoint
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions). [Full Markdown](../../../../docs/webex-connect-api-endpoints-and-regions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the API base URL associated with the API family and the region in which your organization is hosted.

## Selected section

## Select the correct endpoint

The Webex Developer Portal is globally available, but your organization and its assets are hosted regionally. The operation in the API Reference displays the base URL and version supported for the selected environment.

### Digital Channel Onboarding APIs

For Digital Channel Onboarding APIs, use the following base URL for the region in which your organization is hosted:

| Region | Environment | Digital Channel Onboarding API base URL |
| --- | --- | --- |
| Ireland | `prodeu2` | `https://assetmanagement.eu.webexconnect.io/connectapi` |
| Oregon | `produs1` | `https://assetmanagement.us.webexconnect.io/connectapi` |
| London | `prodeu1` | `https://assetmanagement.uk.webexconnect.io/connectapi` |
| Canada | `prodca1` | `https://assetmanagement.ca.webexconnect.io/connectapi` |
| Sydney | `prodanz1` | `https://assetmanagement.au.webexconnect.io/connectapi` |
| Singapore | `prodsg1` | `https://assetmanagement.sg.webexconnect.io/connectapi` |
| India | `prodind1` | `https://assetmanagement.in.webexconnect.io/connectapi` |
| Japan | `prodjp1` | `https://assetmanagement.au.webexconnect.io/connectapi` |

The Sydney and Japan environments currently use the same Digital Channel Onboarding API base URL.

Do not construct a Digital Channel Onboarding API hostname by copying the hostname used by another Webex Connect API family. Use the complete base URL shown for the Digital Channel Onboarding operation and keep it configurable in your application.

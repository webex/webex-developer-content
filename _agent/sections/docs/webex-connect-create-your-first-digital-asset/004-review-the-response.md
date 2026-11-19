---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Review the response
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset). [Full Markdown](../../../../docs/webex-connect-create-your-first-digital-asset.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use the Digital Channel Onboarding APIs to programmatically create supported channel assets for your organization.

This guide shows how to try the APIs by creating an Email asset using a personal access token and the corresponding API Reference operation.

## Selected section

## Review the response

A successful operation returns `200 OK` and can include `assetDetails` together with `code`, `description`, and `transid`. Save the asset identifier and transaction ID needed for later retrieval or troubleshooting.

If the request fails:

- use `400` details to correct the query, header, or body;
- obtain a current token for `401`;
- verify the asset scope, organization access, and user permission for `403`; or
- retain `transid` and `trackingid` when reporting a `500` error.

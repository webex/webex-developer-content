---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Create and authorize a Service App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Create and authorize a Service App

1. Create a [Service App](https://developer.webex.com/admin/docs/service-apps) in Webex for Developers.
2. Request the `spark-admin:datasource_read` and `spark-admin:datasource_write` scopes to show the data-source settings.

   ![Active spark-admin:datasource_read and spark-admin:datasource_write scope choices before selection in the new Service App form.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt74da9bd4945585b9/6aee32f5bf422f9af6f1c272/data-source-scopes-active.jpg)

   *Data-source scope choices before selection in the new Service App form.*
3. Enter a data exchange domain owned by the Service App owner that contains the gRPC endpoint. Do not include a port.
4. Select the Media Forking schema shown when you set up the Service App.

   ![New Service App form with the active audio_forking_schema option selected.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f8ab72fa35db464/6aee32848923da4cbd4ab510/media-forking-schema-active.jpg)

   *Example: `audio_forking_schema` selected in a new Service App form.*
5. Make the Service App visible to the target organization. Request admin authorization for the developer's own organization; for a non-affiliated customer organization, submit the app to Webex App Hub for review.
6. Ask a Full Admin of the customer organization to review and authorize the Service App in Control Hub.

   ![Control Hub displays the Media Forking Dev Sample app with Authorized enabled.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt892353e71f033239/6aee21da38745e032c661e6f/service-app-authorized.jpg)

   *Example of a Service App already authorized in Control Hub.*
7. Obtain the organization-specific Service App access and refresh tokens.
8. Store the app credentials and tokens securely.

Do not use a schema identifier copied from another integration. Use the Media Forking schema selected when you set up this integration.

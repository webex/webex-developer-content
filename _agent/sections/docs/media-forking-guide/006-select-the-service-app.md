---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Select the Service App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Select the Service App

Select the authorized Service App directly in the **Start Media Stream** activity. Media Forking does not require a separate configuration under **Contact Center > Integrations > Features**.

![Start Media Stream activity settings show Media Forking Dev Sample (Service App) as the Media destination.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcbbaf07f0d10d428/6aee21bdc7335a8917274ec6/service-app-media-destination.jpg)

*Example media destination; select the Service App authorized for your organization.*

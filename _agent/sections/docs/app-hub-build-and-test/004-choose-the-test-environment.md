---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-build-and-test
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Choose the test environment
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-build-and-test). [Full Markdown](../../../../docs/app-hub-build-and-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Continue to submission and customer setup](006-continue-to-submission-and-customer-setup.md)

## Article introduction

Turn your chosen app type into a working customer workflow. Plan the components and permissions, build a small working version, and test setup, everyday use, and recovery before preparing your App Hub submission.

## Selected section

## Choose the test environment

Use the [Suite Sandbox](https://developer.webex.com/app-hub/docs/developer-sandbox-guide) for supported Webex Suite workflows or the [Contact Center Sandbox](https://developer.webex.com/app-hub/docs/sandbox_cc) for Contact Center testing. Check each sandbox's prerequisites and available features; access to a sandbox does not enable every API or app type.

Use separate identities for the app developer, customer administrator, and end user when those roles differ. Keep test data separate from customer production data. For BYOVA, also confirm the provider guide's feature and licensing prerequisites for the target organization.

A successful test in your own organization does not prove that another organization can authorize the app. For Service Apps, follow the documented App Hub submission and review path before requesting authorization in another organization. Plan that later validation without assuming the initial private app can perform it.

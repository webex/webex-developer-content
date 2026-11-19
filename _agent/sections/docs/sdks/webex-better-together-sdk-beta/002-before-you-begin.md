---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Overview and limitations](001-overview-and-limitations.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## Before you begin

- Complete the [Webex Contact Center SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart) and [Authentication](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication) setup.
- Use a Contact Center organization provisioned for Webex Together / wxApp telephony. Confirm with your Cisco contact that the organization's Webex-side notification settings are enabled.
- Sign in to the Contact Center station using an **Extension** or **Agent DN**. Browser/WebRTC-only station login is not supported for this answer flow.
- Run Webex App desktop version 44.12 or later on the same computer as the host application, signed in as the same user.
- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use the beta feedback channel shared with your invitation.

Webex Better Together is not gated by a Contact Center user or organization feature toggle. The `enableWxBetterTogether` setting is a separate SDK initialization flag, defaults to `false`, and must be set to the boolean value `true` before SDK initialization, registration, and station login.

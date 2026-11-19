---
type: Excerpt
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Background Image REST Endpoints
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/working-with-device-background-images). [Full Markdown](../../../../docs/working-with-device-background-images.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for Background Images](001-prerequisites-for-background-images.md)

## Article introduction

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

## Selected section

## Background Image REST Endpoints

Background image REST endpoints are found on the [Webex Developer Portal](https://developer.webex.com/), but can be called using Postman, or integrated into code or scripts.

Three REST endpoints exist for handling background images:

- **Upload**: Upload a new background image.
- **List:** List existing background images.
- **Delete**: Delete existing images.

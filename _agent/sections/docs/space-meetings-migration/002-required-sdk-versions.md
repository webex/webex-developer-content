---
type: Excerpt
canonical_url: https://developer.webex.com/docs/space-meetings-migration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Required SDK Versions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/space-meetings-migration). [Full Markdown](../../../../docs/space-meetings-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This documentation describes the upcoming changes in meetings workflow functionality for the mobile and web SDKs. It also includes links to detailed migration documentation.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/space-meetings-migration>) and sign in.

## Selected section

## Required SDK Versions

Please make a note of the required SDK versions and their dates of release.

**Minimum Web SDK Version:** 2.60.0. Contains the new API `reclaimHost()`.

**Minimum Mobile SDK Version:** 3.11.0. Contains the new APIs `reclaimHost()`, `makeHost()`, and `inviteParticipant()`.



> **Info**
>
> Creating instant meetings using the SDKs will be unavailable from version 3.11.0 for mobile SDKs and 2.60.0 for the web SDK. Going forward you'll need to use the public APIs.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/space-meetings-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
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

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-api-and-sdk-support-policy
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Current End of Life (EOL) Notices
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-api-and-sdk-support-policy). [Full Markdown](../../../../docs/webex-api-and-sdk-support-policy.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the current Webex API and SDK support policies.

## Selected section

## Current End of Life (EOL) Notices

### XML API Deprecation

- [XML API Deprecation Announcement](https://developer.webex.com/docs/webex-xml-api-deprecation-announcement)

### SOAP API Deprecation

Due to reasons of security and maintainability we are going to deprecate the recordings SOAP API. In effect Jan 1, 2023 the recordings SOAP API is being deprecated and should not be used for any new projects.
On June 30, 2023 the recordings SOAP API will be permanently shut down. This means customers have a full 6 months to migrate from the current recordings SOAP API to the alternative REST APIs.
Depending on your use cases we recommend using the [/recordings REST resource](https://developer.webex.com/docs/api/v1/recordings). Other functionality in the current SOAP API is replaced by the following APIs: [Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants), [Meetings Chat](https://developer.webex.com/docs/api/v1/meeting-chats), [Meetings Polls](https://developer.webex.com/docs/api/v1/meeting-polls), [Meetings Q&A](https://developer.webex.com/docs/api/v1/meeting-q-and-a)

**Publish date**: 12/27/2022

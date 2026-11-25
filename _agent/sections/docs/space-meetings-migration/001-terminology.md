---
type: Excerpt
canonical_url: https://developer.webex.com/docs/space-meetings-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Terminology
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/space-meetings-migration). [Full Markdown](../../../../docs/space-meetings-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This documentation describes the upcoming changes in meetings workflow functionality for the mobile and web SDKs. It also includes links to detailed migration documentation.



To request or manage this sandbox, open the [official portal page](<https://developer.webex.com/docs/space-meetings-migration>) and sign in.

## Selected section

## Terminology

This table defines the terminology we'll be referencing in this article:



| **Term**              | **Description**                                              |
| --------------------- | ------------------------------------------------------------ |
| **USM Meeting** | Unified Space Meetings a.k.a. [Improved Meetings associated with a Space](https://help.webex.com/en-us/article/gxw5jz/Webex-App-%7C-Improved-meetings-associated-with-a-space) are a subset of meetings happening on the advanced Webex Suite Meetings platform. These meetings use the new suite backend and happen in spaces.  |
| **Create a meeting**  | When a meeting is generated using the [/meetings](https://developer.webex.com/docs/api/v1/meetings) public API. |
| **Start a meeting**   | When a meeting link is used to start a meeting as the first participant. |
| **Join a meeting**    | When a meeting link is used to join an on-going meeting as a subsequent participant. |
| **Space meeting**     | When a meeting is created using [/meetings](https://developer.webex.com/docs/api/v1/meetings) with `roomId` = `<base64Id of room>` and `adhoc = false`. |
| **Instant meeting**   | When a meeting is created using [/meetings](https://developer.webex.com/docs/api/v1/meetings) with `roomId` = `<base64Id of room>` and `adhoc = true`. |
| **Scheduled meeting** | When a meeting is created using [/meetings](https://developer.webex.com/docs/api/v1/meetings) with `roomId` = `<empty>` and `adhoc = false`. |

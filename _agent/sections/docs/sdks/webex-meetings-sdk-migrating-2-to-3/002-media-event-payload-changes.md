---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Media Event Payload Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-migrating-2-to-3.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the migration process for developers who are moving their Webex Web SDK applications from version 2 to version 3. It provides information on the most important changes to the SDK to aid our existing developers in making their applications compatible with SDK version 3.

## Selected section

## Media Event Payload Changes

### 2.x

In the version 2 SDK, the `media:ready` and `media:stop` events on the meeting object return a payload containing the following media types:

- `remoteVideo`
- `remoteAudio`
- `remoteShare`
- `localShare`

The second part of the payload includes `MediaStream` object.

### 3.x

In version 3 SDK, the `localShare` media type is no longer passed as a type in the media event payload.

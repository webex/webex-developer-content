---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Media Effect Upgrades and Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-migrating-2-to-3.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the migration process for developers who are moving their Webex Web SDK applications from version 2 to version 3. It provides information on the most important changes to the SDK to aid our existing developers in making their applications compatible with SDK version 3.

## Selected section

## Media Effect Upgrades and Changes

### 2.x

In version 2 of the SDK, the `meeting` object exposes the Background Noise Removal (BNR) functionality to developers. To enable or disable this functionality, after adding audio tracks to the meeting:

```javascript
meeting.enableBNR();
meeting.disableBNR();
```

### 3.x

In version 3 of the SDK, developers have access to additional media effects features:

- Background Noise Removal
- Custom Virtual Background
- Blur

All the above effects are now exposed as their own classes via the SDK. These effects are applied to the `Stream` objects created at the start of the meeting flow.

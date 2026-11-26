---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify that USM is Enabled
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for USM](002-prerequisites-for-usm.md)

## Article introduction

Webex Meeting today has three distinct meeting experiences: Personal Meeting Rooms (PMR), Scheduled Meetings, and Space Meetings. Each of those meeting types has distinct experiences. Unified Space Meetings (USM) consolidates the experiences of Space Meetings with Webex Meetings and melds them together.

This article explains how to enable USM, how to start ad-hoc meetings, including information on password and captcha support.

## Selected section

## Verify that USM is Enabled

To verify that USM is enabled, check to see that the following statement returns `true`:

```js
webex.meetings.config.experimental.enableUnifiedMeetings;
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Reclaim the host role
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](011-limitations.md)

## Article introduction

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Selected section

## Reclaim the host role

A participant can reclaim host privileges in the meeting by using the [assignRoles](https://webex.github.io/webex-js-sdk/api/#membersassignroles) method within the members object. The code snippet below illustrates its use.

```javascript
  const selfId = meeting.members.selfId;
  const role = {
    type: 'MODERATOR',
    hasRole: true,
    hostKey,
  };

  meeting.members.assignRoles(selfId, [role])
```

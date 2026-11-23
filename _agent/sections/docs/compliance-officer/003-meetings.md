---
type: Excerpt
canonical_url: https://developer.webex.com/docs/compliance-officer
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/compliance-officer). [Full Markdown](../../../../docs/compliance-officer.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Compliance Officers can access and manage organization content with dedicated authorization scopes. Learn how data ownership, room permissions, and meeting recordings affect that access.

## Selected section

## Meetings

Please refer to the [Meetings](https://developer.webex.com/docs/meetings) documentation for details.

### Meeting Recordings

Compliance officers are able to retrieve user recordings for analysis and compliance. There is a separate API endpoint for admins and compliance officers [/admin/recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings-for-an-admin-or-compliance-officer), while regular users use [/recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings). As it relates to recording deletion, a recycle bin and associated recording `status` is available. A user typically moves a recording to the recycle bin via the GUI and then either restores the recording or purges the recording from the recycle bin. Once purged, the recording isn't accessible to regular users any longer, but it is still accessible to the Compliance Officer until it is removed through the retention process. Compliance officers who want to retrieve user-deleted recordings must query the [/events API](https://developer.webex.com/docs/api/v1/events) for deleted recording events, and use the returned recording ID to retrieve the recording from [/recordings/{id}](https://developer.webex.com/docs/api/v1/recordings/get-recording-details). Regular users will see a 404 error.

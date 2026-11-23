---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-programming-interface-behavior-changes
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- What you should do
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-programming-interface-behavior-changes). [Full Markdown](../../../../docs/app-programming-interface-behavior-changes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This page highlights recent API behavior changes associated with the upgrade to the Webex Suite Meeting Platform.

---

Developers have reported unexpected changes in functionality, such as [join links](https://developer.webex.com/docs/api/v1/meetings/join-a-meeting) requiring authentication and the [meeting chats API](https://developer.webex.com/docs/api/v1/meeting-chats) not returning new results.

If you encounter any of these issues, open a ticket with our [support team](mailto:devsupport@webex.com) so we can validate your environment and recommend the best path forward.

These changes are a byproduct of the ongoing migration of customer sites to the Webex Suite Meeting Platform (WSMP).

## Selected section

## What you should do

- If you’re using meetings join links for automation, validate the authentication requirements for your meeting type and site.
- If you rely on meeting chat content for compliance or DLP/CASB use cases, validate your `/events` consumption for `meetingMessages`.
- If you rely on meeting polls or Q&A reporting, plan to use Sli.do APIs.
- If you rely on meeting transcripts, validate whether Cisco AI Assistant is enabled for the meeting.

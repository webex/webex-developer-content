---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webinar-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Adding and managing panelists
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webinar-guide). [Full Markdown](../../../../docs/webinar-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

As a Webex developer you now have the ability to manage webinars using the webinar REST APIs to create and manage a Webex webinar, and well as add and manage webinar panelists.

---

# Webinar

Use Webex Webinar with Meetings REST API.

## Selected section

## Adding and managing panelists

Developers can use [Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees) API to manage webinar panelists. For webinars, all the invitees will join as panelists. Panelists can also be added using the [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API by specifying invitees in the request body. The following new boolean attribute needs to be enabled to mark an invitee as a panelist:

* `panelist` – When set as an attribute in a `POST` request body, specifies whether an invitee is allowed to be a panelist for the webinar.

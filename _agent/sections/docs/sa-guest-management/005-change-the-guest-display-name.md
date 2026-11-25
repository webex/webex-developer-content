---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sa-guest-management
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Change the Guest Display name
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sa-guest-management). [Full Markdown](../../../../docs/sa-guest-management.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Management happens via Service Apps in order to provide unlicensed users with temporary access to Webex functionality. 

## Selected section

## Change the Guest Display name

If you want to change your guest displayName, you do the `POST` to `/guests/token` with an already used `subject` and the new `displayName`.
Remember that most Webex Applications retain history. So if you change the `displayName` between users but keep the `subject,` they may potentially see their respective space or call history.

To change the display name of a guest user who has already authenticated, simply re-authenticate with a new guest token. After authenticating via the API or with the SDKs with the new guest token, the guest user's display name will be updated.

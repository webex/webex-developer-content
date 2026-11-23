---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sa-guest-management
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Refresh the Guest Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sa-guest-management). [Full Markdown](../../../../docs/sa-guest-management.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Management happens via Service Apps in order to provide unlicensed users with temporary access to Webex functionality. 

## Selected section

## Refresh the Guest Token

If your guest `Access Token` did expire and you want to keep the guest, you can create a new one by doing the `POST` to `/guests/token` with an existing `subject`. If the old token has life left, it won’t be revoked. Each user in Webex can have no more than 750 tokens, and this applies equally to guests.

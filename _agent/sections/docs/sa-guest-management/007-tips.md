---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sa-guest-management
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Tips
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sa-guest-management). [Full Markdown](../../../../docs/sa-guest-management.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Management happens via Service Apps in order to provide unlicensed users with temporary access to Webex functionality. 

## Selected section

## Tips

Guests are created in their own organization for security purposes. While the guest `id` is a `personId`, the Service App and you as an admin cannot delete that guest. The Service App or admin cannot delete [authorizations](https://developer.webex.com/admin/docs/api/v1/authorizations). Guest tokens age out on their own, and there is no limit to the number of guests. [Contact Support](https://developer.webex.com/support) if you need to delete guests.

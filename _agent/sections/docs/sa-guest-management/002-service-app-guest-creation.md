---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sa-guest-management
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Service App Guest Creation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sa-guest-management). [Full Markdown](../../../../docs/sa-guest-management.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Management happens via Service Apps in order to provide unlicensed users with temporary access to Webex functionality. 

## Selected section

## Service App Guest Creation

Before you can create guest tokens, you will need to create a new Service App in [My Webex Apps](https://developer.webex.com/my-apps) for use by your system. Make sure you have, at a minimum, the `guest-issuer:write` and `guest-issuer:read` scopes selected which are used for guest management. Only paid Webex subscribers may create guests.

For a **new** Service App with no legacy Guest Issuer, org admin authorization is followed by `POST /v1/guests/token`—you do **not** need the bind step described on [Guest Issuer Migration Guide](https://developer.webex.com/docs/guest-issuer-migration).

This Service App must be approved by an admin in Control Hub. To that end, you will need to submit your app for admin approval by a *Full Admin* within your organization. Or, if you want to create guests for other organizations, you will need to submit your Service App to AppHub. Do note, though, that Guests are always created in their own independent organization that has little relationship to the organization of the Service App or the organization of the approver.

For details on the approval process and subsequent retrieval of the `Access Token` and `Refresh Token,` please see the [Service App Guide](https://developer.webex.com/docs/service-apps)

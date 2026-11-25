---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webinar-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Registration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webinar-guide). [Full Markdown](../../../../docs/webinar-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

As a Webex developer you now have the ability to manage webinars using the webinar REST APIs to create and manage a Webex webinar, and well as add and manage webinar panelists.

---

# Webinar

Use Webex Webinar with Meetings REST API.

## Selected section

## Registration

Developers can use the [Create Meeting](https://developer.webex.com/docs/api/v1/meetings) API to create and manage registration for a webinar, as well as enable/disable the auto-approval process for registrants by setting the `autoAcceptRequest` attribute value in the `POST` request body. In addition to that, the following APIs are available to manage registration:

* [Get the registration form definition for a webinar](https://developer.webex.com/docs/api/v1/meetings/get-registration-form-for-a-meeting) - Get a webinar's registration form to understand which fields are required for an attendee's registration.
* [Add a webinar registrant](https://developer.webex.com/docs/api/v1/meetings/register-a-meeting-registrant) - Used for registering a new registrant for a webinar.
* [Get and list webinar registrants](https://developer.webex.com/docs/api/v1/meetings/list-meeting-registrants) - Used for retrieving details of a webinar registrant with a specified registrant Id. Can also be used to retrieve a list of registrants for a webinar with a specified meeting Id.
* [Batch update the status of webinar registrants](https://developer.webex.com/docs/api/v1/meetings/batch-update-meeting-registrants-status) - A webinar's host or cohost can batch update the status of registrants.

The following roles can `register` an attendee via the API up to the capacity limit for a webinar:
* The host of the webinar
* The cohosts of the webinar
* Any user of the same site
* The administrator of the site where this webinar is hosted
* [Guests](https://developer.webex.com/docs/guest-issuer)

The following roles can approve or reject a pending registrant for a webinar:
* The host of the webinar
* The cohosts of the webinar

The following roles can `invite` an attendee using the API up to the license capacity limit by the host license:
* The host of the webinar
* The cohosts of the webinar
* Any user of the same site
* The administrator of the site where this webinar is hosted

Developers should note that registration capacity has a maximum limit of 10K. There's no minimum limit, which means that a webinar can support any number of invitees or registrations fewer than 10K.

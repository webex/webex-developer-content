---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webinar-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating and managing a Webex Webinar
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webinar-guide). [Full Markdown](../../../../docs/webinar-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

As a Webex developer you now have the ability to manage webinars using the webinar REST APIs to create and manage a Webex webinar, and well as add and manage webinar panelists.

---

# Webinar

Use Webex Webinar with Meetings REST API.

## Selected section

## Creating and managing a Webex Webinar

Webinars can be created, retrieved, updated, and deleted using the [Meetings](https://developer.webex.com/docs/api/v1/meetings) API. The following new attributes have been introduced for scheduling a webinar:

* `scheduledType` – When set as an attribute in a `POST` request body, specifies either webinar or a regular meeting. Set the value of `scheduledType` attribute to `webinar` for scheduling a webinar, and to `meeting` for scheduling a regular meeting. This attribute is mandatory for scheduling a webinar.
* `enabledWebcastView` – Set the value of `enabledWebcastView` attribute in a `POST` request body to `true` for scheduling a streaming mode for a webinar and to `false` for scheduling an interactive mode for a webinar. The default value for this attribute is `false`.
* `panelistPassword` – When set as an attribute in a `POST` request body, specifies the password for panelists of Webinar. The password must conform to the site's password complexity settings as described in [password management](https://help.webex.com/en-us/zrupm6/Manage-Security-Options-for-Your-Site-in-Webex-Site-Administration). If not specified, a random password conforming to the site's password rules is generated automatically.
* `phoneAndVideoSystemPanelistPassword` – When returned as an attribute in a `GET` request, specifies the 8-digit numeric panelist password to join a webinar from audio and video devices.

Developers should note that a webinar cannot be updated to a regular meeting and vice-versa. Also, developers can get and list [Meeting Session Types](https://developer.webex.com/docs/api/v1//meetings/sessionTypes) enabled for a given user for scheduling a meeting or webinar. In addition to that, the following attributes are not supported for a webinar:

* `recurrence`
* `allowFirstUserToBeCoHost`
* `allowAuthenticatedDevices`
* `excludePassword`
* `enableAutomaticLock`

---
type: Guide
title: Webinar Developer Guide | Consolidated Guide
display_title: Webinar Guide
canonical_url: https://developer.webex.com/docs/webinar-guide
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webinar-guide)

As a Webex developer you now have the ability to manage webinars using the webinar REST APIs to create and manage a Webex webinar, and well as add and manage webinar panelists.

---

# Webinar

Use Webex Webinar with Meetings REST API.

## Overview

As a Webex host, you can schedule engaging, interactive [webinars](https://help.webex.com/en-US/article/n3rosq0/Get-started-with-Webex-Events-(new)), and Webex developers now have the ability to manage webinars using REST APIs.

The webinar REST API includes the following features:

* [Create and manage a Webex webinar](https://developer.webex.com/docs/api/v1/meetings)
* [Add and manage webinar panelists](https://developer.webex.com/docs/api/v1/meeting-invitees)
* [Get and list meeting session types for scheduling the type of meeting](https://developer.webex.com/docs/api/v1/meetings)
* [Get a registration form definition for a webinar](https://developer.webex.com/docs/api/v1/meetings/get-registration-form-for-a-meeting)
* [Add a webinar registrant](https://developer.webex.com/docs/api/v1/meetings/register-a-meeting-registrant)
* [Get and list webinar registrants](https://developer.webex.com/docs/api/v1/meetings/list-meeting-registrants)
* [Batch update the status of webinar registrants](https://developer.webex.com/docs/api/v1/meetings/batch-update-meeting-registrants-status)

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

## Adding and managing panelists

Developers can use [Meeting Invitees](https://developer.webex.com/docs/api/v1/meeting-invitees) API to manage webinar panelists. For webinars, all the invitees will join as panelists. Panelists can also be added using the [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API by specifying invitees in the request body. The following new boolean attribute needs to be enabled to mark an invitee as a panelist:

* `panelist` – When set as an attribute in a `POST` request body, specifies whether an invitee is allowed to be a panelist for the webinar.

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

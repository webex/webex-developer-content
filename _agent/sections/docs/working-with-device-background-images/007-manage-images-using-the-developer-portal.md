---
type: Excerpt
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage Images Using the Developer Portal
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/working-with-device-background-images). [Full Markdown](../../../../docs/working-with-device-background-images.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for Background Images](001-prerequisites-for-background-images.md)

## Article introduction

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

## Selected section

## Manage Images Using the Developer Portal

You can easily manage background images at different levels in the Developer Portal using the associated REST APIs. Begin by logging in and grabbing your temporary developer access token for your account by navigating to the [Access the Webex API](https://developer.webex.com/docs/getting-started) page. Save the token and use it the REST API calls described in the following sections. In addition, you can also use the developer portal **Try it** mode to experiment with APIs as well. If you’re new to REST APIs or need a quick refresher, see [REST API Basics](https://developer.webex.com/docs/basics).



> **Info**
>
> A developer access token is provided for testing purposes only! Never use it in production since it expires 12 hours after being generated, or upon logging out of the Webex Developer Portal.



### Configure an Image URL Using the REST API at an Organization or Location Level

To configure an image URL using the REST API at an organization or location level see the following API entries:

- To update the background image, see [POST Device Settings](https://developer.webex.com/docs/api/v1/device-call-settings/change-device-settings-across-organization-or-location-job).
- To read configuration for a location, see [GET Location Device Settings](https://developer.webex.com/docs/api/v1/device-call-settings/get-location-device-settings).
- To read configuration for an organization, see [GET Org Device Settings](https://developer.webex.com/docs/api/v1/device-call-settings/read-the-device-override-settings-for-a-organization).

### Configure an Image URL Using the REST API at a Device Level

To configure an image URL using the REST API at a device level see the following API entries:

- To update the background image, see [PUT Device Settings](https://developer.webex.com/docs/api/v1/device-call-settings/update-device-settings).
- To read the configuration, see [GET Device Settings](https://developer.webex.com/docs/api/v1/device-call-settings/get-device-settings).



> **Info**
>
> Devices do not automatically apply changes. To make changes take effect right away, manually select **Apply Changes** in Control Hub, use a developer REST API to initiate it for each device, wait for the nightly resync, or reboot/power cycle the device.

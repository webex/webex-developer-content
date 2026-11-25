---
type: Excerpt
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Delete Images Using the Delete REST Endpoint
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/working-with-device-background-images). [Full Markdown](../../../../docs/working-with-device-background-images.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for Background Images](001-prerequisites-for-background-images.md)

## Article introduction

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

## Selected section

## Delete Images Using the Delete REST Endpoint

Use the `delete` endpoint to delete the list of designated device background images for an organization. You can delete a maximum of 10 images per request.

API details can be found here: [DELETE Background Images](https://developer.webex.com/docs/api/v1/device-call-settings/delete-device-background-images).

When deleting an image keep the following points in mind:

- If `forceDelete` is set to false or is not specified, and the custom background URL is configured with the image being deleted at the device, location, or organization level, the request is rejected.
- If `forceDelete` is set to true, and the custom background URL is configured with the image being deleted at the device, location, or organization level, the background image configuration will be set to None at those levels. The change to None will be applied to devices when "Apply changes" is requested for the device, during the nightly resync, or upon reboot or power cycle of the phone. The image will still be visible on any phone that was configured until None has been applied.

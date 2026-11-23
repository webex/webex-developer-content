---
type: Excerpt
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Upload Image Using the Upload REST Endpoint
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/working-with-device-background-images). [Full Markdown](../../../../docs/working-with-device-background-images.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for Background Images](001-prerequisites-for-background-images.md)

## Article introduction

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

## Selected section

## Upload Image Using the Upload REST Endpoint

The upload endpoint adds a new background image file for the entire organization to use and sets up a device to display it. After uploading, a resync request is sent to the device to display the new background image.



> **Info**
>
> The Upload API requires a device to be identified. As part of the upload this device will be configured to use the uploaded image so that the image can be validated for correct presentation on that device.



The upload endpoint uses a multipart/form-data request with two entries:

- `name=”file”` where `file` is the name of the image file on the uploading computer.
- `name="filename"` where `filename` is the name you want to use for the uploaded image in Webex.

Example:

```text
Body: multipart/form-data
--aBoundaryString
Content-Disposition: form-data; name="file"; fileName=<name of file on computer>
Content-Type: <png | jpg>
<image binary>
--aBoundaryString
Content-Disposition: form-data; name="fileName"
<name to call the uploaded image>
--aBoundaryString
```

API details can be found here: [POST Upload Background Image](https://developer.webex.com/docs/api/v1/device-call-settings/upload-a-device-background-image)



> **Info**
>
> Uploading an image to a device configures that device to use the image as a device-level override. This configuration applies even if the rest of the device’s settings are taken from the organization or location level. Because this is a device-level configuration, subsequent changes to background images at the organization or location level do not affect this device until the device-level background image is removed. This can be done by configuring the device to "Define custom device settings," saving it, and then returning it to "Use the location settings," and saving that.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites for Background Images
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/working-with-device-background-images). [Full Markdown](../../../../docs/working-with-device-background-images.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

## Selected section

## Prerequisites for Background Images

Before continuing, verify your Cisco device compatibility as well as your background image format and size constraints as follows:

### Supported Devices

- 8800 series (all except 8875)
- 6871

#### Supported Image Sizes per Model

- 8811: greyscale - 480x128
- 8832: color - 480x128
- Other 8800 series: color - 800x480
- 6871: color - 480 x 272

### Supported Image formats:

- PNG
- JPG

### Maximum File Size

- 625 KB



> **Info**
>
> Although devices can adjust image sizes, ensuring the correct aspect ratio yields optimal results.

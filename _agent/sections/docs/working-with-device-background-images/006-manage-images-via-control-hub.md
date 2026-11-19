---
type: Excerpt
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Manage Images via Control Hub
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/working-with-device-background-images). [Full Markdown](../../../../docs/working-with-device-background-images.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for Background Images](001-prerequisites-for-background-images.md)

## Article introduction

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

## Selected section

## Manage Images via Control Hub

You can easily configure uploaded images to devices at different levels using Webex Control hub.

### Configure an Image URL using Control Hub at an Organization Level

To configure an image URL using Control Hub at a organization level:

1. Log in to [Control Hub](https://admin.webex.com/) with your administrator credentials.
1. Navigate to the **Calling** section.
1. Move to the **Service Settings** tab.
1. Select **Configure Default Device Settings**.
1. Under **MPP Device Settings,** set the **Background Image** option to **Custom Background**.
1. Configure the URL of the file in the **Custom Background** URL field and save it.



> **Info**
>
> Org-level device settings are ineffective if either the device's location has custom settings defined (location-level overrides) or the device itself has custom settings defined (device-level overrides).



### Configure an image URL using Control Hub at Location Level

To configure an image URL using Control Hub at a location level:

1. Log in to [Control Hub](https://admin.webex.com/) with your administrator credentials.
1. Navigate to the **Location List** section.
1. Select the location you want to update.
1. Move to **Calling** section.
1. In the **Device Management** card, click **Manage**.
1. Choose **Define Custom Device Settings**.
1. Under **MPP Device Settings,** set Background Image option to Custom Background.
1. Configure the URL of the file in **the Custom Background URL** field and save it.



> **Info**
>
> Location level device settings do not apply to devices in the location if the device’s Device settings has Define custom device settings selected (device level overrides are configured).



### Configure an Image URL using Control Hub at a Device Level

To configure an image URL using Control Hub at a device level:

1. Log in to [Control Hub](https://admin.webex.com/) with your administrator credentials.
1. Navigate to the **Devices List** section.
1. Select the **Device** you want to update.
1. In **Device Management** card, click on **Device Settings Manage**.
1. Choose **Define Custom Device Dettings**.
1. Set **Background Image** option to **Custom Background**.
1. Configure the URL of the file in **Custom Background URL** text field and save it.



> **Info**
>
> The **Apply Changes** action isn't automatic for devices. To apply changes right away, manually request it in Control Hub or use the Developer API for each device. Alternatively, you can wait for the nightly resync, or reboot or power cycle the phone.

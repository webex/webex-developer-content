---
type: Guide
title: Working with Device Background Images | Consolidated Guide
display_title: Background Images
canonical_url: https://developer.webex.com/docs/working-with-device-background-images
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/working-with-device-background-images)

Webex Calling supports the upload of up to 100 background image files for each organization. These image files can then be referenced by Cisco MPP devices in that org for use as their background image.

---

This article describes how to manage images using Webex Control Hub as well as the Webex REST APIs.

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



## Background Image REST Endpoints

Background image REST endpoints are found on the [Webex Developer Portal](https://developer.webex.com/), but can be called using Postman, or integrated into code or scripts.

Three REST endpoints exist for handling background images:

- **Upload**: Upload a new background image.
- **List:** List existing background images.
- **Delete**: Delete existing images.

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



## List Images Using the List REST Endpoint

List the images that are uploaded and ready for use. API details can be found here: [GET Background Image List](https://developer.webex.com/docs/api/v1/device-call-settings/read-the-list-of-background-images)

## Delete Images Using the Delete REST Endpoint

Use the `delete` endpoint to delete the list of designated device background images for an organization. You can delete a maximum of 10 images per request.

API details can be found here: [DELETE Background Images](https://developer.webex.com/docs/api/v1/device-call-settings/delete-device-background-images).

When deleting an image keep the following points in mind:

- If `forceDelete` is set to false or is not specified, and the custom background URL is configured with the image being deleted at the device, location, or organization level, the request is rejected.
- If `forceDelete` is set to true, and the custom background URL is configured with the image being deleted at the device, location, or organization level, the background image configuration will be set to None at those levels. The change to None will be applied to devices when "Apply changes" is requested for the device, during the nightly resync, or upon reboot or power cycle of the phone. The image will still be visible on any phone that was configured until None has been applied.

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

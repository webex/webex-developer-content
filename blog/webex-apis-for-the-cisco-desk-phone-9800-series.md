---
type: Article
title: Webex APIs for the Cisco Desk Phone 9800 Series
canonical_url: https://developer.webex.com/blog/webex-apis-for-the-cisco-desk-phone-9800-series
content_type: blog
date: '2025-08-07'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-apis-for-the-cisco-desk-phone-9800-series)

Devices in the [Cisco Desk Phone 9800 Series](https://www.webex.com/us/en/devices/phone-series/cisco-phone-9800-series.html) have a robust feature set, with brilliant audio &amp; video quality, enhanced security, and user-friendly designs. The 9800 Series runs on the [PhoneOS](https://help.webex.com/en-us/article/n1trwjh/Release-Notes-for-Cisco-PhoneOS-Phones-9800-and-8875) operating system that provides flexible control and scalability in modern cloud-based collaboration environments. This makes the Desk Phone 9800 Series ideal for enterprises seeking robust, programmable, and future-proof communication solutions.

When used in a Webex Calling environment, Cisco 9800 Series phones deliver a seamless and intuitive communication experience that simplifies device management through centralized control. This enables efficient configuration updates, policy enforcement, and bulk changes across locations or the entire organization without the need for physical access to each phone.

What also makes these phones a preferred choice for enterprises are the flexible administration capabilities via the Webex Calling APIs, that can automate lifecycle management, customization, and post-activation configurations on devices. This article will detail how the Webex Calling APIs can be leveraged for integrations that automate the setup and configuration of Cisco 9800 Series phones. While we are mainly focusing on 9800 Series, the APIs covered in this article also pertain to the [Cisco Video Phone 8875](https://www.webex.com/us/en/devices/phone-series/cisco-video-phone-8875.html), which also runs on PhoneOS.

The first section highlights key distinctions between Cisco 9800-series phones and Cisco MPP devices, to clarify some of the notable differences in how they are respectively set up and managed. In the second section, we go through the Webex Calling APIs for the 9800 Series phones, grouped into specific feature categories for easier understanding and usage.

### Cisco 9800 Series (PhoneOS) vs. Cisco Multiplatform Phones (MPP)

For those who have previously managed Cisco Multiplatform Phones (MPP) devices, there are some important differences to note when setting up and configuring a Cisco 9800 Series (PhoneOS) device. The main aspects of the 9800 Series and MPP devices are compared in the table below.

<table>
<tr>
<td>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</td>
<td>

<strong>Cisco Desk Phone 9800-Series</strong>&nbsp;&nbsp;&nbsp;&nbsp;
</td>
<td>

<strong>Cisco Multiplatform Phone (MPP)<strong>&nbsp;&nbsp;&nbsp;&nbsp;
</td>
</tr>
<tr>
<td>

<em>Operating System</em>
</td>
<td>

PhoneOS, a modern, unified OS designed for cloud and hybrid use.
</td>
<td>

MPP firmware, legacy platform.
</td>
</tr>
<tr>
<td>

<em>Provisioning</em>
</td>
<td>

Supports zero-touch provisioning via activation codes and APIs.
</td>
<td>

More configurations possible before activation; conventional provisioning methodology.
</td>
</tr>
<tr>
<td>

<em>Configuration Timing</em>
</td>
<td>

Many configurations require the device to be online to apply changes via APIs.
</td>
<td>

More pre-activation configuration possible before device is online.
</td>
</tr>
<tr>
<td>

<em>API Support</em>
</td>
<td>

Extensive Webex Calling APIs for device and call settings.
</td>
<td>

Limited API support; more manual or CUCM-based configuration.
</td>
</tr>
<tr>
<td>

<em>Feature Set</em>
</td>
<td>

Integrated with Webex ecosystem, supports desk reservation, hot desking, AI noise removal, and advanced security features.
</td>
<td>

Supports core calling features; fewer integrated collaboration features.
</td>
</tr>
<tr>
<td>

<em>Management</em>
</td>
<td>

Managed primarily via Cisco Control Hub and Webex Calling APIs.
</td>
<td>

Managed via CUCM or legacy management tools.
</td>
</tr>
</table>

As you can see, one of the very significant differences Is the “Configuration Timing” of the two platforms. With MPP, most settings can be preconfigured before the device is online, including provisioning files and settings pushed prior to registration. In PhoneOS, phones must *first* come online and communicate their capabilities before most configuration options can be set. This means *after* plugging-in a phone, entering an activation code, and then waiting for a reboot. Most configurations, such as applying line key templates, device settings, and layout modifications, can be done via APIs after the PhoneOS device is online and registered.

Another key aspect is that Cisco MPP OS does not support the broad range of Webex Calling APIs that are available for PhoneOS devices. This means many of the APIs mentioned here are limited or unavailable for MPP devices. Conversely, PhoneOS devices are designed to be extensively managed and configured through the Webex Calling APIs after activation and registration.

It’s also important for developers to note that 9800 Series phones (PhoneOS) are referenced in Webex API calls by the Device ID value: `deviceId`, which is generated for any Webex Device as it connects to Webex. Conversely, MPP and third-party phones are referenced in API calls by the Webex Calling Device ID: `callingId`, which is the unique identifier for a device within the scope of calling services.

For context, the example JSON snippet below shows that the [Get Device Details API](https://developer.webex.com/calling/docs/api/v1/devices/get-device-details) returns both the device `id` and `callingId` of a registered 9800 Series phone. The device `id` is the value used in subsequent API calls to configure and manage the phone.

```json
{
"items": [
    {
      "id": "Y2lzY29sd42gdvfsfxxxxxxx" , //deviceId
      "webexId": "Y2lzY29zcGFyazovL3Vybxxxxxxx",
      "callingId": "Y2lzY29zcGFyazovL3Vybjxxxxxxx" ,
      "displayName": "Phil's Desk Phone",
      "placeId": "YTQ0LTRmZwQt0GZjYS05ZGY0YjRmNDE3Zjxxxxxxx",
      "workspaceId": "YTQ0LTRmZWQt0GZjYS05ZGY0YjRmNDE3ZjUxxxxxxxx",
      "personId": "YTQ0LTRmZWQt0GZjYS05ZGYOYjRmNDE3ZjUxxxxxxx",
      "orgId": "LTEXZTUtYTE1M11mZTM00DE5Y2RjOWExxxxxxxx",
      ...
      ...
      ...
    }
  ]
}
```

Next up is a walkthrough of the Webex Calling APIs that are available for the 9800 Series Phones, grouped into general feature categories.

### Webex Calling APIs for the Cisco 9800 Series (PhoneOS)

This section explores the Webex Calling APIs for [Devices](https://developer.webex.com/calling/docs/api/v1/devices), [Device Call Settings](https://developer.webex.com/calling/docs/api/v1/device-call-settings), and [Device Configurations](https://developer.webex.com/devices/docs/api/v1/device-configurations) that are used to set up and configure 9800 Series phones. Again, the APIs are grouped by feature categories here to highlight how they are generally used by device integrations.

#### 1. Device Lifecycle Management APIs

This first set of Calling APIs help manage the registration, activation, and inventory of phones, which is the first step before 9800 Series devices can be configured:

- [Create a Device Activation Code](https://developer.webex.com/calling/docs/api/v1/devices/create-a-device-activation-code)
  - *Use Case: Generate an activation code to enable zero-touch provisioning for a new phone, allowing automatic registration with Webex Calling upon first power-up.*
- [Create a Device by MAC Address](https://developer.webex.com/calling/docs/api/v1/devices/create-a-device-by-mac-address)
  - *Use Case: Register a new phone by its MAC address and assign it to a user or workspace before a physical deployment.*
- [Delete a Device](https://developer.webex.com/calling/docs/api/v1/devices/delete-a-device)
  - *Use Case: Remove decommissioned or lost phones to free licenses and prevent unauthorized use.*
- [Get Device Details](https://developer.webex.com/calling/docs/api/v1/devices/get-device-details)
  - *Use Case: Retrieve detailed data about a phone’s configuration, capabilities, status, and assigned user.*
- [List Devices](https://developer.webex.com/calling/docs/api/v1/devices/list-devices)
  - *Use Case: Obtain an inventory list of all registered phones for management.*
- [Modify Device Tags](https://developer.webex.com/calling/docs/api/v1/devices/modify-device-tags)
  - *Use Case: Update metadata tags to classify phones by location, department, or usage for easier filtering.*
- [Validate a List of MAC Addresses](https://developer.webex.com/calling/docs/api/v1/device-call-settings/validate-a-list-of-mac-address)
  - *Use Case: Verify batches of MAC addresses before provisioning to ensure device validity and support.*

<br/>

#### 2. Device Configuration and Settings APIs

This extensive group of Calling APIs is for managing, customizing, and applying configuration settings on Cisco 9800 Series phones. They are classified here in three types – Device Settings, Layout/Line Key Management, and Other Device Configurations. As mentioned earlier, these and the other remaining APIs are utilized after the phone is activated.

**APIs for Device Settings Management** ([help article](https://help.webex.com/en-us/article/uil72l/Configure-and-modify-device-settings-in-Webex-Calling))

The Device Settings APIs enable administrators to centrally manage and customize Cisco phone settings at various scopes – organization, location, workspace, device, and user. Settings include audio, network, security, and feature preferences, among others:

- [Change Device Settings Across Organization or Location Job](https://developer.webex.com/calling/docs/api/v1/device-call-settings/change-device-settings-across-organization-or-location-job)
  - *Use Case: Execute bulk updates for all phones in a location or organization.*
- [Read the Device Override Settings for an Organization](https://developer.webex.com/calling/docs/api/v1/device-call-settings/read-the-device-override-settings-for-a-organization)
  - *Use Case: Retrieve the settings for a phone that can supersede configurations at other levels across the organization.*
- [Get Location Device Settings](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-location-device-settings)
  - *Use Case: Retrieve the custom phone configuration values for a location that supersede the broader organization-wide defaults.*
- [Get Device Settings for a Workspace](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-device-settings-for-a-workspace)
  - *Retrieve the custom phone configuration values for a workspace (office, meeting room, etc.) that supersede the location and organization level defaults.*
- [Update Device Settings for a Workspace](https://developer.webex.com/calling/docs/api/v1/device-call-settings/update-device-settings-for-a-workspace)
  - *Use Case: Enable hot desking or modify settings for all phones in a shared workspace.*
- [Get Device Settings](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-device-settings)
  - *Use Case: Retrieve the custom configuration values for a specific phone that supersede the workspace, location, and organization level defaults.*
- [Update Device Settings](https://developer.webex.com/calling/docs/api/v1/device-call-settings/update-device-settings)
  - *Use Case: Remotely apply settings changes, such as call handling preferences or line key assignments.*
- [Apply Changes for a Specific Device](https://developer.webex.com/calling/docs/api/v1/device-call-settings/apply-changes-for-a-specific-device)
  - *Use Case: Prompt a phone to download and apply an updated configuration.*
- [Get Device Settings for a Person](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-device-settings-for-a-person)
  - *Use Case: Retrieve the custom phone configuration values for a user, some of which may supersede the defaults on other levels.*
- [Update Device Settings for a Person](https://developer.webex.com/calling/docs/api/v1/device-call-settings/update-device-settings-for-a-person)
  - *Use Case: Modify user-specific settings like call forwarding or line appearances.*

<br/>

**APIs for Device Layout and Line Key Template Management**
(layout [help article](https://help.webex.com/en-us/article/g19k2r/Create-and-manage-line-key-templates), templates [help article](https://help.webex.com/en-us/article/g19k2r/Create-and-manage-line-key-templates))

**This set of APIs** are used to create and bulk assign templates to phone layouts using line key templates. These are used to customize layout modes for various functionalities like line appearances, speed dials, and feature access:

- [Modify Device Layout by Device ID](https://developer.webex.com/calling/docs/api/v1/device-call-settings/modify-device-layout-by-device-id)
  - *Use Case: Customize the programmable line keys (PLK) on a phone, to match a specific layout based on the user role.*
- [Get Device Layout by Device ID](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-device-layout-by-device-id)
  - *Use Case: Retrieve the PLK information from a phone to verify or audit the current button layout of a phone.*
- [Create a Line Key Template](https://developer.webex.com/calling/docs/api/v1/device-call-settings/create-a-line-key-template)
  - *Use Case: Define a custom button layout template to standardize line keys across a department.*
- [Apply a Line Key Template](https://developer.webex.com/calling/docs/api/v1/device-call-settings/apply-a-line-key-template)
  - *Use Case: Quickly configure a phone’s button layout by applying a predefined template.*
- [Modify a Line Key Template](https://developer.webex.com/calling/docs/api/v1/device-call-settings/modify-a-line-key-template)
  - *Use Case: Update existing templates to add or remove buttons based on user needs.*
- [Delete a Line Key Template](https://developer.webex.com/calling/docs/api/v1/device-call-settings/delete-a-line-key-template)
  - *Use Case: Remove obsolete templates to maintain a clean configuration environment.*
- [Get Details of a Line Key Template](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-details-of-a-line-key-template)
  - *Use Case: Fetch the current line key template details, including key labels, functions, and layout, to ensure consistent and up-to-date device configurations across the organization.*
- [Preview Apply Line Key Template](https://developer.webex.com/calling/docs/api/v1/device-call-settings/preview-apply-line-key-template)
  - *Use Case: Simulate template application to verify changes before deployment.*
- [Read the List of Line Key Templates](https://developer.webex.com/calling/docs/api/v1/device-call-settings/read-the-list-of-line-key-templates)
  - *Use Case: List all available templates for selection or modification.*

<br/>

**APIs for Other Device Configuration** ([help article](https://help.webex.com/en-us/article/n72q8yeb/Configure-9800-Series-and-8875-Phones-on-Control-Hub))

This unique set of APIs are more commonly used to configure RoomOS devices but can also manage certain configuration settings on Cisco 9800 Series phones:

- [List Device Configurations for device](https://developer.webex.com/devices/docs/api/v1/device-configurations/list-device-configurations-for-device)
  - *Use Case: Retrieve the current configuration settings of a Series 9800 phone by its deviceId, such as phone lines, softkeys, network settings, directory services, power saving features, SIP and audio settings, custom wallpaper, firmware updates, and other device behaviors.*
- [Update Device Configurations](https://developer.webex.com/devices/docs/api/v1/device-configurations/update-device-configurations)
  - *Use Case: Automate bulk configuration changes to ensure consistent settings across phones.*

<br/>

#### 3. Workspace Devices APIs

The Workspace Devices APIs allows administrators to manage and audit Webex Calling devices in fixed workspaces, including the 9800 Series. This facilitates the monitoring and administration of phones used in collaborative environments, like meeting rooms:

- [Get Workspace Devices](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-workspace-devices)
  - *Use Case: Retrieve devices assigned to shared workspaces to automate inventory audits.*
- [Modify Workspace Devices](https://developer.webex.com/calling/docs/api/v1/device-call-settings/modify-workspace-devices)
  - *Use Case: Manage hot desking by adding or removing devices from shared workspaces.*

<br/>

#### 4. Device Members and Hoteling APIs

The Device Members APIs allows the identification and management of phones and other calling devices assigned to specific *users* or *workspaces* within the organization. The Hoteling APIs manages the feature that allows users to temporarily load their phone profile onto a shared (host) phone, enabling them to make calls with their work number and access their calling features from any designated host device. When used together, these APIs are especially useful for managing shared phones in flexible workspaces, such as a hot-desking or co-working environments:

- [Get Device Members](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-device-members)
  - *Use Case: Fetch device membership information to verify correct user assignments, detect unauthorized changes, or prepare for device reassignments.*
- [Search Members](https://developer.webex.com/calling/docs/api/v1/device-call-settings/search-members)
  - *Use Case: Search for users or members to associate with devices or apply user-specific settings.*
- [Update Members on the Device](https://developer.webex.com/calling/docs/api/v1/device-call-settings/update-members-on-the-device)
  - *Use Case: Add or remove members from shared lines or group call features.*
- [Get Person Devices](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-person-devices)
  - *Use Case: Audit user device assignments to enable targeted configuration, troubleshooting, or call settings management on the devices linked to that person.*
- [Modify Hoteling Settings for a Person’s Primary Devices](https://developer.webex.com/calling/docs/api/v1/device-call-settings/modify-hoteling-settings-for-a-person-s-primary-devices)
  - *Use Case: Assign or modify hoteling hosts and configure association time limits programmatically.*

<br/>

#### 5. Job and Monitoring APIs

This group confirms the status for device configuration changes and applying templates. This helps diagnose if there are any failures in these processes, for efficient device management and operational reliability:

- [Get the Job Status of an Apply Line Key Template Job](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-the-job-status-of-an-apply-line-key-template-job)
  - *Use Case: Monitor the progress and completion of line key template application jobs, ensuring that the changes have been successfully applied or to reveal any issues during the process.*
- [Rebuild Phones Configuration](https://developer.webex.com/calling/docs/api/v1/device-call-settings/rebuild-phones-configuration)
  - *Use Case: Trigger a rebuild job on phones in a location if the network configuration switches from “public” to “private” and vice versa.*
- [Get the Job Status of a Rebuild Phones Job](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-the-job-status-of-a-rebuild-phones-job)
  - *Use Case: Track the status a phone rebuilding job to confirm it has been completed successfully.*
- [Get Job Errors for an Apply Line Key Template Job](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-job-errors-for-an-apply-line-key-template-job)
  - *Use Case: Retrieve the `trackingID` of an error when a line key template job fails, for further troubleshooting.*
- [Get Job Errors for a Rebuild Phones Job](https://developer.webex.com/calling/docs/api/v1/device-call-settings/get-job-errors-for-a-rebuild-phones-job)
  - *Use Case: Obtain error reports for phone rebuild jobs to troubleshoot issues.*
- [List Change Device Settings Jobs](https://developer.webex.com/calling/docs/api/v1/device-call-settings/list-change-device-settings-jobs)
  - *Use Case: List all device settings change jobs for audit and tracking*.
- [List Change Device Settings Job Errors](https://developer.webex.com/calling/docs/api/v1/device-call-settings/list-change-device-settings-job-errors)
  - *Use Case: View errors associated with device settings change jobs.*
- [List Rebuild Phones Jobs](https://developer.webex.com/calling/docs/api/v1/device-call-settings/list-rebuild-phones-jobs)
  - *Use Case: Retrieve all phone rebuild jobs to monitor configuration refresh activities.*

<br/>

### Check Out Our Vidcast

<br/>


	<iframe src="https://app.vidcast.io/share/embed/7b9ad3f2-24eb-483c-87d2-e8003c23ed43?disableCopyDropdown=1" width="100%" height="100%" title="Webex APIs for the Cisco Desk Phone 9800 Series" loading="lazy" allow="fullscreen *;autoplay *;" style="position: absolute; top:0; left: 0; border: solid; border-radius: 12px;"></iframe>


<br/>

### We Are Here to Help!

We are always eager to provide support for these Calling APIs and integrations. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Until next time, happy integration building!

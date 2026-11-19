---
type: Guide
title: What's New
display_title: What's New
canonical_url: https://developer.webex.com/docs/whats-new-calling
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/whats-new-calling)

We want to make sure that you know about the major updates made available in Webex Calling APIs.

---

For information on all new features and functionality of Webex Calling, please visit this page on the [Webex Help Center](https://help.webex.com/en-us/article/rdmb0/What's-new-in-Webex-Calling#wbxc_r_whats_new_2023).

## August 2024

What's new for August 2024...

### August 23, 2024

#### Provisioning API:  Select PSTN provider for a location
Adds ability to get list of potential Cloud Connected PSTN Providers (CCPP) for a given location, select a specific provider for that location, and query the PSTN connection type for a location.

### August 21, 2024

#### Provisioning API:  Service Numbers for Premise-based PSTN

Added support for _Service Numbers_, local telephone numbers considered as high utilization or concurrent, making them ideal for assignment to high-volume services such as Auto Attendants, Hunt Groups, and Call Queues. The [**Add Numbers**](https://developer.webex.com/docs/api/v1/numbers/add-phone-numbers-to-a-location), [**Get Numbers**](https://developer.webex.com/docs/api/v1/numbers/get-phone-numbers-for-an-organization-with-given-criterias), and [**Initiate Number**](https://developer.webex.com/docs/api/v1/numbers/initiate-number-jobs) Jobs APIs are modified to support service numbers. Additionally, feature-specific available numbers APIs such as Hunt Group, Location, Person, and Workspace have been added to help identify numbers that can be associated with specific members or features. These feature-specific APIs are streamlined with fewer parameters, making them more easily to use as alternatives to the more general [**Get Numbers**](https://developer.webex.com/docs/api/v1/numbers/get-phone-numbers-for-an-organization-with-given-criterias) API.

## July 2024

What's new for July 2024...

### July 17, 2024

#### Provisioning API: Device API improved usability

The Device API now accepts the "product" value in /telephony/config "model" fields for improved consistency and usability. 

#### Provisioning API:  Call Recording Additions

Expanded capability of Call Recording APIs to include setting Call Recording Vendor at organization and location levels, Call Recording terms of service, and retrieving organizational & location level Call Recording vendors and vendor users.

### July 15, 2024

#### Provisioning API: Emergency Services

Exposed APIs for management of Emergency Services settings, including emergency call notification, emergency callback number for users, virtual lines, and workspaces.  

## May 2024

What's new for May 2024...

### May 30, 2024

#### Provisioning API: Workspace Call Settings

Added multiple endpoints to enable management of all _Professional Workspace_ call settings.

## April 2024

What's new for April 2024...

### April 20, 2024

#### Provisioning API: Device Configuration - Phase 3

Added ability to configure line key settings per device, retrieve devaice details, update device compression settings, rebuild phones, and retrieve the IP address of the device.

#### Provisioning API: DECT Devices - Phase 2

Expanded DECT API to obtain DECT network, base station and handset details, update configuration, and delete elements.

## March 2024

What's new for March 2024...

### March 8, 2024

#### Provisioning API: Ability to Manage Virtual Lines Call Settings

Added the ability to manage Virtual Lines Call Settings like Voicemail, Music on Hold, Push to Talk, Call Bridge, Barge In and Privacy Settings. For details, see [Virtual Line Call Settings](https://developer.webex.com/docs/api/v1/virtual-line-call-settings).

## January 2024

What's new for January 2024...

### January 25, 2024

#### Provisioning API: Ability to Add and Manage Virtual Lines

Added the ability to add and manage Virtual Lines, their devices, numbers, and directory searches. Also added the ability to configure a subset of Virtual Line calling settings, including Caller ID, Call Forwarding, Call Waiting, Incoming Permission, Outgoing Calling Permissions, and Call Intercept.

## October 2023

What's new for October 2023...

### October 23, 2023

#### Device API: Ability to search for a device by MAC address

Ability to list a device by querying on its MAC address.

## August 2023

What's new for August 2023...

### August 31, 2023

#### Provisioning API: Ability to list and add Webex Calling Devices and Workspaces

Ability to list and add Webex Calling Workspaces and Devices, Device Call Settings with Third-party device activation. Additionally, ability to view/add/change/remove phone number, extension, and locationId to a Workspace.

#### Provisioning API: Device Line Key Template

Adding support for Devices Configuration API to manage Line Key Templates, in the Webex for Developers Platform.

## July 2023

What's new for July 2023...

### July 31, 2023

#### API Provisioning: Enhancement to Custom Contact Group List

Webex Calling now allows adding location features like Hunt Group to the custom contact group list via API. The list is visible in the Receptionist Client.

### July 27, 2023

#### API to select Preferred Device for call handling

With the increase in use of Webex clients and hybrid work environments, it’s desirable for end users to choose their preferred device to handle API-based call handling. This feature provides a capability to let the administrator or end user select the device to use for auto answer and Remote Control forced answer.

### July 7, 2023

#### API Provisioning: Announcement Repository

Adding support for administrators to create an organization-level pool of announcements and media. For details, see [Announcement Repository](https://developer.webex.com/docs/api/v1/features-announcement-repository).

## May 2023

What's new for May 2023...

### May 17, 2023

#### Provisioning API: Device Activation

Adding support for Device activation. This API allows administrators to add or remove Webex Calling Devices to Webex Calling users and places.

## April 2023

What's new for April 2023...

### April 11, 2023

#### Support for Webex Calling API

You can now access the Webex Calling APIs using Service Apps. To start using the Service Apps, see Using Webex Service Apps.

## Coming Soon

This section describes features in development that will be coming soon.

#### Provisioning API: User Selective Services

Adding support for retrieving and configuring the Selective Call Acceptance, Call Forwarding, and Call Rejections for a user, including rules and schedules to apply specific settings.

#### Provisioning API: Single Device Settings Partial Customization

Ability to set a device field value without causing all fields to be customized/disassociated from the location-level settings if provisioned using a location template.

#### Provisioning API: CX Essentials Call Queues, Agents and Supervisors

Adding support for enabling Call Queue Agents and Supervisors of _CX Essentials_.

## Known Issues

Issues with Webex Calling APIs will be listed here until they are resolved.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/device-developers-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What can I use these APIs for?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/device-developers-guide). [Full Markdown](../../../../docs/device-developers-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## Selected section

## What can I use these APIs for?

Using these APIs, you can automate things that take up a significant amount of an administrator's time every day. Think about use cases like these:

- Roll out a new setting to a group of devices with e.g. an "earlyAdopters" tag
- Generate a daily report of all devices with issues
- Make a dashboard that shows which of your devices are in use, how many are presenting content, how many people are using them and what type of workspaces they are located in
- Automatically set the type and capacity of all your workspaces based on their names
- Calculate a weekly report showing the total workspace capacity of your organization

The devices APIs expose hundreds of configurations, commands and statuses to interact with. The devices upload schema to the cloud that define the configurations, commands and statuses they support, so if a device upgrades and gets new features they are instantly available through the Device APIs.

The powerful part of this REST interface is the ability for developers and administrators to perform these actions without having direct network access to the devices, regardless of device location. This would allow them to perform actions and resolve issues on devices in home offices without physically going there. You can read and write configurations while the device is offline and any changes you make will then be applied as soon as the device comes back online. The communication channel between the REST interface and the device is encrypted.

Take a look at our [Webex Device APIs example scripts](https://github.com/CiscoDevNet/webex-device-api-examples) on Cisco DevNet for help on how to use these APIs and ideas on what to do with them.

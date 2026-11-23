---
type: Excerpt
canonical_url: https://developer.webex.com/docs/devices
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Giving a bot or user access to the xAPI of a device
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/devices). [Full Markdown](../../../../docs/devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## Selected section

## Giving a bot or user access to the xAPI of a device

An integration operates on behalf of a user. If this user is not an administrator of the devices in the organization, they must be explicitly granted device authorizations to the APIs just as with bots. Bots are only able to make API calls to devices which are registered in the same organization as the user who created a bot.

Your system administrator sets up device authorizations through the Cisco Webex Control Hub ([https://admin.webex.com](https://admin.webex.com)). Authorization for a bot or user is given for a *Workspace*, not a *Device*. If there are multiple devices associated with a Workspace, all these devices get the same authorization.

Inform your system administrator about the email address of your bot, so that they can set up the authorizations. They must repeat the following process for each workspace that has devices that your application is going to interact with:

1. From the customer view in [https://admin.webex.com](https://admin.webex.com), go to the *Workspaces* page. Search for the Workspace that contains the devices that you want to give the bot API access to. Click this Workspace to view the details.
2. In the Devices card, click *Edit API Access*. A list of all bots and users with authorization to access the API of the devices opens.
3. Click the plus sign (+) to add a new authorization. Choose the user or bot account that you want to authorize for the Workspace and select the appropriate access level. *Full Access* means that the user or bot can read device details, invoke commands and query status. *Read Only* means that the user or bot can only read device details and query status.

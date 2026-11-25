---
type: Excerpt
canonical_url: https://developer.webex.com/docs/device-developers-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating an application that can access the Webex REST API
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

## Creating an application that can access the Webex REST API

In general, you can create either a [Bot](https://developer.webex.com/docs/bots) or an [Integration](https://developer.webex.com/docs/integrations). A bot cannot work across different organizations, it will only work on devices that belong to the same organization as the creator of the bot. In addition, a bot can only access devices to which it has been specifically granted access. Bots are useful for applications that are intended to be used in one organization and possibly need to be restricted to only a subset of devices. An integration, on the other hand, can perform actions on behalf of a user. Developers who wish to build applications that will work for multiple organizations, should create an integration. Administrators from multiple organizations can authorize an integration to perform actions on their behalf, and the integration will be able to access all devices in the organization(s) that the administrator(s) belong to.

The Device Configuration API and the Workspaces API are restricted to only allow administrators, not bots. That means you can try out the APIs using the [Device Configuration API Reference](https://developer.webex.com/docs/api/v1/device-configurations) and [Workspaces API Reference](https://developer.webex.com/docs/api/v1/workspaces), but in order to provide functionality for admin users to call this API you will need to create an integration that can act on behalf of them.

If you are new to creating Webex applications, check out [this blog post](https://blogs.cisco.com/developer/webex-teams-apis-awesome) to get started with REST API calls to the Webex platform.

### For Integrations

Reference the [integration documentation](https://developer.webex.com/docs/integrations) to learn how to make integrations.

In order to create an integration that can make Device API calls, your integration needs to request one or more of the following scopes:

- `spark:devices_read` - See details for your devices
- `spark:devices_write` - Modify and delete your devices
- `spark-admin:devices_read` - Read devices and device configurations in your organization
- `spark-admin:devices_write` - Create, update and delete devices and device configurations in your organization
- `spark-admin:workspaces_read` - See details for workspaces you manage.
- `spark-admin:workspaces_write` - Create, modify, and delete workspaces you manage.
- `spark:xapi_commands` - Execute commands towards devices and query command schemas
- `spark:xapi_statuses` - Query status on devices and query status schemas

### For Bots

To create a bot that can make device calls:

1. Log in to <https://developer.webex.com>, select *My Webex Apps* from the menu under your avatar at the top of this page.
2. Click *Create a New App*, followed by *Create a Bot* to start the wizard. Fill in the registration form (Bot name, Bot Username, Icon, Description), and click *Add Bot*. As the logged in user, you own the bot account, and the bot belongs to the same organization as you.
3. Copy the Access Token you receive for the new bot and keep it somewhere safe. You must always use this token to authenticate your bot with the Webex REST API. If lost, you have to generate a new one: Select *My Webex Apps* from the menu, select your bot, and click *Regenerate Access Token*.

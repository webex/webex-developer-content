---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.generalNotifications (Application Notifications)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-widget-data-layout). [Full Markdown](../../../../docs/desktop-widget-data-layout.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Connect custom widgets to Desktop data through STORE properties and JSON layout configuration.

## Parent context

## Data Provider—Widget Properties and Attributes

**Note:** To receive real-time data through properties or attributes inside a custom widget, it has to be assigned appropriately in the layout JSON configuration by the administrator. For more information on JSON layout, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

In addition to accessing data through JavaScript SDK subscribers, you can request data to be passed also through properties or attributes. If your component is built to react to changes in property or attribute, you will always get updated data this way from the single source of truth, the Desktop. We call it a data provider.

Currently, we have a single data provider under the key STORE. Below, you will find a breakdown of all possible data and type definitions that is available through the STORE key:

- STORE.agent
- STORE.agentContact
- STORE.app
- STORE.auth
- STORE.generalNotifications
- STORE.dynamic

## Selected section

### STORE.generalNotifications (Application Notifications)

| Name                                                    | Type    | Description                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| STORE.generalNotifications.isNotificationsEnabled       | Boolean | Determines whether the display of notifications is enabled or disabled on the Desktop. <br> - True—Enables the display of notifications on the Desktop. <br> - False—Disables the display of notifications on the Desktop.                                                                                                                                    |
| STORE.generalNotifications.isSilentNotificationsEnabled | Boolean | Determines whether the display of visual notifications is enabled or disabled on the Desktop. <br> - True—Enables the display of visual notifications on the Desktop. <br> - False—Disables the display of visual notifications on the Desktop. <br> **Note:** Silent notifications do not display on the Desktop, but are listed in the Notification Center. |
| STORE.generalNotifications.countActivated               | Number  | The number of active notifications displayed on the Desktop.                                                                                                                                                                                                                                                                                                  |
| STORE.generalNotifications.countDeactivated             | Number  | The number of notifications that are not active. The Notification Center icon displays a badge indicating the number of unread notifications displayed on the Desktop.                                                                                                                                                                                        |
| STORE.generalNotifications.countPending                 | Number  | The number of active notifications that are displayed on the Desktop before the notification pop-up is closed.                                                                                                                                                                                                                                                |
| STORE.generalNotifications.countAdded                   | Number  | The total number of all notifications displayed on the Desktop.                                                                                                                                                                                                                                                                                               |

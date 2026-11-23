---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agentContact.taskMap.Task.interaction.callAssociatedData
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

### STORE.agentContact.taskMap.Task.interaction.callAssociatedData

| Name          | Type    | Description                                                                                                                                                                                                     |
| ------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| displayName   | String  | Label for the Call-Associated Data (CAD) variable. For example, Customer Address.                                                                                                                               |
| name          | String  | Key (unique identifier) for the CAD variable.                                                                                                                                                                   |
| agentEditable | Boolean | Determines whether an agent can edit a CAD variable during an active call. <br>- True—Agent can edit a CAD variable during an active call. <br> - False—Agent cannot edit a CAD variable during an active call. |
| value         | String  | Value of the CAD variable.                                                                                                                                                                                      |
| type          | String  | Data type of the call variable value. The CAD variable types are Boolean, String, Integer, Decimal, or Date Time.                                                                                               |

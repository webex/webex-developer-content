---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agentContact (Tasks/Interactions)
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

### STORE.agentContact (Tasks/Interactions)

| Name                                  | Type   | Description                                                                                                                 |
| ------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| STORE.agentContact.lastCompletedTask  | String | Unique Identifier for the last wrapped up task.                                                                             |
| STORE.agentContact.selectedTaskId     | String | Unique Identifier for the selected task.                                                                                    |
| STORE.agentContact.interactionIds     | Array  | List of Unique identifiers of the user interactions.                                                                        |
| STORE.agentContact.chatConferenceData | Object | Options of the chat conference data. For more information, see [STORE.agentContact.chatConferenceData](https://developer.webex.com/docs/desktop-widget-data-layout#storeagentcontactchatconferencedata).                       |
| STORE.agentContact.taskMap            | Map    | The full list of tasks that are assigned to an agent at a given time. For more information, see [STORE.agentContact.taskMap](https://developer.webex.com/docs/desktop-widget-data-layout#storeagentcontacttaskmap). |
| STORE.agentContact.taskSelected       | Object | Provides the user interaction details of the selected task.                                                                 |

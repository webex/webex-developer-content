---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agentContact.taskMap.Task.interaction
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

### STORE.agentContact.taskMap.Task.interaction

| Name                  | Type   | Description                                                                                                                                 |
| --------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| mediaType             | String | The media channel type. The possible values are telephony, social, email, and chat.                                                         |
| state                 | String | Current agent state.                                                                                                                        |
| participants          | Object | Map keyed by participant ID, with details about each participant.                                                                                   |
| interactionId         | String | Unique identifier for the user interaction.                                                                                                 |
| orgId                 | String | Unique identifier of the organization.                                                                                                      |
| callProcessingDetails | Object | Options from the acceptance of an incoming call through the final disposition of the call. For more information, see callProcessingDetails. |
| media                 | Object | Options of the digital media. For more information, see media.                                                                              |
| owner                 | String or Null | Unique identifier for an agent who owns the interaction.                                                                                    |
| mediaChannel          | String | The media channel type. The possible values are telephony, social, email, and chat.                                                         |
| contactDirection      | Object | Options of the call type from a dialer to recipient.                                                                                        |
| -->type               | String | Call type from a dialer to recipient. The possible values are OUTBOUND and INBOUND.                                                         |
| outboundType          | String or Null | Type of an outdial call such as OUTDIAL, COURTESY_CALLBACK and CAMPAIGN; null for inbound interactions.                                                                    |
| callFlowParams        | Object | Options of the call flow parameters. For more information, see callFlowParams.                                                              |
| callAssociatedData    | Object | Options of the Call-Associated Data (CAD) variables For more information, see callAssociatedData.                                           |

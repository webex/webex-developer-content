---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agentContact.taskMap.Task.interaction.media
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

### STORE.agentContact.taskMap.Task.interaction.media

| Name            | Type           | Description                                                                                                                                                          |
| --------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| mediaResourceId | String         | Unique identifier of the digital channel.                                                                                                                            |
| mediaType       | String         | The media channel type. The possible values are telephony, social, email, and chat.                                                                                  |
| mediaMgr        | String         | Refers to the media manager.                                                                                                                                         |
| participants    | Array          | List of participants with details about each participant.                                                                                                            |
| mType           | String         | Specifies whether the digital channel incoming request is from an original call (call between a customer and an agent who accepted a customer call) or consult call. |
| isHold          | Boolean        | Determines whether the customer call is put on hold or not. <br>- True—Customer is put on hold. <br> - False—Customer call is not put on hold.                       |
| holdTimestamp   | Number or Null | The timestamp displays the time when a call is put on hold.                                                                                                          |

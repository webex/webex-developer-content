---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agent.wrapUpData
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

### STORE.agent.wrapUpData

| Name                     | Type                 | Description                                                                                                                                                                                                                                                            |
| ------------------------ | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| wrapUpProps              | Object               | Options of the wrap up property.                                                                                                                                                                                                                                       |
| -->autoWrapup            | Boolean or Undefined | Determines whether the auto wrap up is enabled or not. <br> - True—The auto wrap up is enabled.<br> - False—The auto wrap up is disabled.                                                                                                                              |
| -->autoWrapupInterval    | Number or Undefined  | Indicates the count down time that is left before the interaction is auto wrapped up.                                                                                                                                                                                  |
| -->wrapUpReasonList      | Array                | The array of objects. For more information, see wrapUpReasonList.                                                                                                                                                                                                      |
| -->interactionId         | String               | Unique identifier for the user interaction.                                                                                                                                                                                                                            |
| -->allowCancelAutoWrapup | Boolean or Undefined | Determines whether an agent can cancel the Desktop from wrapping up automatically. <br> - True—Enables an agent to cancel the auto wrap up time and extend the wrap up time. <br>- False—Disables an agent to cancel the auto wrap up time and extend the wrap up time. |

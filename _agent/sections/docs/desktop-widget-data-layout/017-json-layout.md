---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- JSON Layout
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

### JSON Layout

```json
{
"widgets": {
    "my-component": {
        "comp": "my-custom-component",
        "properties": {
            "agentDnNumber": "$STORE.agent.dnNumber",
            "channelsStatesMap": "$STORE.agent.channelsStatesMap",
            "teamId": "$STORE.agent.teamId"
        }
    }
}
}
```

**Note:** With granular state control, the global **$STORE.agent.subStatus** is not valid. Consume agent state from **$STORE.agent.channelsStatesMap** instead.

| Name                 | Type   | Description                                                                                                                                                                                    |
| -------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| widgets              | Object | Refers to custom widgets.                                                                                                                                                                      |
| my-component         | Object | Refers to custom components.                                                                                                                                                                   |
| comp                 | String | Represents the name of the custom HTML element (known as Web Component or any other element).                                                                                                  |
| properties           | Object | Specifies the properties that you need to pass for a Web Component.                                                                                                                            |
| -->agentDnNumber     | String | Dial Number (DN) used for inbound and outbound calls.                                                                                                                                          |
| -->channelsStatesMap | Object | Map of channel-level agent state (keyed by channel type). With granular state control, consume agent state from this; global **subStatus** is not valid. Use for agent status and **stateChangeTimestamp** per channel.  |
| -->teamId            | String | Unique identifier of the team.                                                                                                                                                                 |

For more information on JSON layout, see [Create custom desktop layout](https://help.webex.com/en-us/article/ng08gqeb/Create-custom-desktop-layout) in Webex Help Center.

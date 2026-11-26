---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agentContact.taskMap
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

### STORE.agentContact.taskMap

| Name                      | Type          | Description                                                                                                                                                                                                                                                       |
| ------------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TaskId                    | String        | Unique identifier for the task.                                                                                                                                                                                                                                   |
| Task                      | Object        | Options of an active request or task or interaction.                                                                                                                                                                                                              |
| -->mediaResourceId        | String | Unique identifier of the digital channel.                                                                                                                                                                                                                                |
| -->agentId                | String        | Unique identifier of the agent.                                                                                                                                                                                                                                   |
| -->destAgentId            | String or Null        | Unique identifier of the chat conference request destination agent. The destination agent refers to another agent who joined the chat.                                                                                                                            |
| -->trackingId             | String        | Unique identifier based on the notification error.                                                                                                                                                                                                                |
| -->consultMediaResourceId | String or Null        | Unique identifier of the chat conference digital channel.                                                                                                                                                                                                         |
| -->interaction            | Object        | Details for the user interaction. For more information, see [STORE.agentContact.taskMap.Task.interaction](https://developer.webex.com/docs/desktop-widget-data-layout#storeagentcontacttaskmaptaskinteraction).                                                                                                                                                          |
| -->interactionId          | String        | Unique identifier for the user interaction.                                                                                                                                                                                                                       |
| -->orgId                  | String        | Unique identifier of the organization.                                                                                                                                                                                                                            |
| -->owner                  | String or Null        | Unique identifier for the agent who owns a task.                                                                                                                                                                                                                  |
| -->queueMgr               | String        | Unique identifier for the queue manager.                                                                                                                                                                                                                          |
| -->type                   | String        | Name of the event that describes the unique notification response. The response is used by an event listener.                                                                                                                                                     |
| -->ronaTimeout            | Number        | Indicates the configured RONA timeout value. <br>**Note:** The maximum available time to accept a voice call request is 18 seconds. The maximum available time to accept a digital channel request is 32 seconds.                                                 |
| -->isConsulted            | Boolean       | Determines whether an agent is consulted by another agent or not. <br> - True—Allows an agent to be consulted by another agent. <br>- False—Prevents an agent from being consulted by another agent.                                                              |
| -->isConferencing         | Boolean       | Determines whether an agent can accept a conference request or not. <br>- True—Allows an agent to accept a conference request.<br> - False—Prevents an agent from accepting a conference request.                                                                 |
| -->updatedBy              | String        | Unique identifier of the agent who updates the Call-Associated Data (CAD) variables of a task.                                                                                                                                                                    |
| -->destinationType        | String        | The type of request to be placed. The destination type can be Agent, Queue, or DN.                                                                                                                                                                                |
| -->autoResumed            | Boolean       | Determines whether the paused call must be resumed manually. <br>- True—Voice call to be resumed automatically after the specified duration. <br> - False—User to take action on the paused voice call based on the button defined. For example, Start Recording. |
| -->reasonCode             | String or Number        | Reason code for an error on the Desktop. For example, ReasonCode 26 (DC_CALLS_LIMIT_EXCEEDED)                                                                                                                                                                     |
| -->reason                 | String        | Reason for an error on the Desktop. For example, ReasonCode 26 is displayed when the data center has reached the maximum limit for concurrent outdial calls.                                                                                                      |

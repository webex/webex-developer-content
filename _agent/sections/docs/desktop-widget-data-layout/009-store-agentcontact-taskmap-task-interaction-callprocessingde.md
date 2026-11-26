---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-widget-data-layout
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Data Provider—Widget Properties and Attributes
- STORE.agentContact.taskMap.Task.interaction.callProcessingDetails
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

### STORE.agentContact.taskMap.Task.interaction.callProcessingDetails

| Name                          | Type   | Description                                                                                                                                                       |
| ----------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ani                           | String | The phone number (Automatic Number Identification) of the customer in case of an inbound call. In the case of email and chat, the email ID of the customer.       |
| dnis                          | String | The phone number (Dialed Number Identification) of the customer care in case of an outdial call.                                                                  |
| tenantId                      | String | Unique database identifier of the tenant (organization).                                                                                                          |
| QueueId                       | String | Unique identifier of the routing queue.                                                                                                                           |
| vteamId                       | String | Unique identifier of the virtual team.                                                                                                                            |
| pauseResumeEnabled            | String | Agent can access the Privacy Shield icon to pause and resume recording a call.                                                                                    |
| pauseDuration                 | String | Specifies the time, in seconds, for which the Desktop pauses the call recording. After the time has elapsed, the Desktop automatically starts recording the call. |
| isPaused                      | String | Indicates whether a call recording is paused or not.                                                                                                              |
| recordInProgress              | String | Indicates whether a call recording is in progress or not.                                                                                                         |
| ctqInProgress                 | String | Indicates whether a consult call to queue is in progress or not.                                                                                                  |
| outdialTransferToQueueEnabled | String | Indicates whether an outdial transfer call to queue is enabled or not.                                                                                            |
| convIvrTranscript             | String | Indicates whether an IVR transcript is available for current user interaction or not.                                                                             |
| customerName                  | String | Name of the customer.                                                                                                                                             |
| virtualTeamName               | String | Name of the virtual customer.                                                                                                                                     |
| ronaTimeout                   | String | Indicates the configured RONA timeout value.                                                                                                                      |
| category                      | String | The value selected by a customer while initiating a chat. The administrator defines the values for an organization.                                               |
| reason                        | String | Reason for a customer to contact the contact center.                                                                                                              |
| sourceNumber                  | String | Unique identifier of a digital channel source. For example, Facebook Messenger source number.                                                                     |
| sourcePage                    | String | Source page of a digital channel. For example, Facebook Messenger source page.                                                                                    |
| appUser                       | String | Unique identifier of a digital channel user. For example, Facebook Messenger user.                                                                                |
| customerNumber                | String | Unique identifier of the customer.                                                                                                                                |
| reasonCode                    | String or Number | Reason code associated with a reason for a customer to contact the contact center.                                                                                |
| IvrPath                       | String | The Interactive Voice Response (IVR) call flow allows a customer to be routed to an appropriate queue.                                                            |
| fromAddress                   | String | Customer email ID for an incoming email.                                                                                                                          |

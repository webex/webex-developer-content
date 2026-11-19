---
type: Guide
title: Call Control Developer Guide | Consolidated Guide
display_title: Call Control
canonical_url: https://developer.webex.com/docs/call-control
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/call-control)

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Overview

This guide provides guidance on service-level integrations with Webex Calling. It covers:

- **Authentication and authorization** via Service Apps
- **Admin-level Call Control APIs** for managing active calls
- **Discovery APIs** for enumerating organization content
- **Telephony WebHooks** for real-time event notifications
- **Interest Registration** for enabling additional webhook events

## Authentication and Authorization

### Service Apps

The Service App concept is how third-party applications can be authorized to perform admin-level call control actions on behalf of an organization.

A Service App declares the scopes it requires. An organization administrator can associate a Service App with its organization, granting it the access specified in the Service App's scopes.

Once granted access, a third-party application can retrieve an access token associated to that Service App. The access token authorizes the third-party application to perform API calls based on its authorized scopes.

For more information about Service Apps, see the [Using Webex Service Apps](https://developer.webex.com/docs/service-apps) guide.

## Call Control APIs

Admin-level call control APIs allow a Service App to retrieve information about active calls and perform actions on them.

The admin-level call control APIs are derived from user-level call control APIs, but with an added `member` URL parameter. A member can be a Person, Workspace, or Virtual Line.

For more information, see the [Call Controls Members API](https://developer.webex.com/docs/api/v1/call-controls-members) documentation.

## Discovery APIs

These APIs are used to discover the content of an organization.

### Member Enumeration

There are three types of calling members. Each member type has its own enumeration API:

| Member Type | API | Notes |
|-------------|-----|-------|
| People | [List People](https://developer.webex.com/docs/api/v1/people/list-people) | Set `callingData=true` to include calling-specific information. Filter non-calling users by inspecting the `licenses` array. |
| Workspaces | [List Workspaces](https://developer.webex.com/docs/api/v1/workspaces/list-workspaces) | Returns all workspaces in the organization |
| Virtual Lines | [Read the List of Virtual Lines](https://developer.webex.com/docs/api/v1/virtual-line-call-settings/read-the-list-of-virtual-lines) | Returns all virtual lines in the organization |

### Call Queue Enumeration

#### Customer Assist and Call Queues

Use the [Read the List of Call Queue or Customer Assist Queues](https://developer.webex.com/docs/api/v1/features-call-queue/read-the-list-of-call-queue-or-customer-assist-queues) API:

| Queue Type | Parameter |
|------------|-----------|
| Customer Assist Queues | `hasCxEssentials=true` |
| Call Queues | `hasCxEssentials=false` |

#### Queue-Agent Assignments

To retrieve the queue assignments of a given agent, use the [Get Details for an Agent for Call Queue or Customer Assist](https://developer.webex.com/docs/api/v1/features-call-queue/get-details-for-an-agent-for-call-queue-or-customer-assist) API with the same `hasCxEssentials` parameter.

## Telephony WebHooks

WebHooks are used across Webex to notify your app about events or activities happening on the Webex platform.

The Webex Calling platform exposes webhook resources. These resources are labeled with the `telephony_` prefix.

For more information about Webex Webhooks, see the [Webhooks Guide](https://developer.webex.com/docs/webhooks).

### Org-Level WebHooks

Telephony Webhooks leverage org-level WebHooks. By registering a WebHook with the `ownedBy` field set to `org`, a Service App can receive the events for all actors in an organization. Only org-level WebHooks are supported for Service Apps. Only a subset of telephony webhooks support org-level webhooks and can therefore be used by Service Apps.

### Telephony Resource Definitions

| Resource | Events | Required Scope | Description |
|----------|--------|----------------|-------------|
| `telephony_calls` | created, updated, deleted | `spark-admin:calls_read` | Notification of calls progression through each state |
| `telephony_agent` | updated | `spark-admin:calls_read` | Notification of call queue agent changes |
| `telephony_agentMonitoring` | updated | `spark-admin:calls_read` | Notification of call queue agent performance metrics |
| `telephony_queue` | updated | `spark-admin:calls_read` | Notification of call queue calls progression |
| `telephony_queueMonitoring` | updated | `spark-admin:calls_read` | Notification of call queue performance metrics |

### Webhook Registration Example

```bash
curl -L --request POST \
  --url 'https://webexapis.com/v1/webhooks' \
  --header 'Authorization: Bearer $ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
    "name": "My agentMonitoring Webhook",
    "targetUrl": "https://example.com/my-endpoint",
    "resource": "telephony_agentMonitoring",
    "event": "all",
    "ownedBy": "org"
  }'
```

For detailed webhook payload schemas and examples, see <a href="#webhook-payload-schemas">Webhook Payload Schemas</a> at the end of this guide.

---


## Interest Registration

Webhook interests enable the emission of Webex Calling webhook events that are not emitted by default, even when a webhook is registered for an applicable resource. Clients manage webhook interests through registrations. Once a client registers an interest, that interest applies to all applicable webhooks for the organization, not only webhooks created by that client. Webhook interests are therefore not intended to filter unwanted events.

Webhook interest registrations expire and should be refreshed periodically. The default expiration period is 60 days.

There are two types of webhook interests: **resource interests** and **actor interests**. Webhook events for actor and resource categories without a corresponding interest type do not require an interest registration and are always emitted.

Although POST and DELETE operations are technically "write" operations, they are exceptionally associated with the `spark-admin:calls_read` scope because they are used alongside the read-only Webhook APIs.

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/telephony/webhookInterestRegistrations` | Create or update a webhook interest registration |
| GET | `/telephony/webhookInterestRegistrations` | Get the current webhook interest registration |
| DELETE | `/telephony/webhookInterestRegistrations` | Delete the webhook interest registration |

**Required Scope:** `spark-admin:calls_read`

### Create a Webhook Interest Registration

**POST** `/telephony/webhookInterestRegistrations`

Creates or updates a webhook interest registration. At least one interest is required.

#### Request Body

| **Property** | **Type** | **Required** | **Description** |
|--------------|----------|--------------|-----------------|
| `interests` | array | Yes | Collection of webhook interests. At least one required. Each interest has either `resource` or `actor` set (not both). |
| `duration` | integer | No | Days until expiration. Defaults to 60 days. |

#### Request Example

```json
{
  "interests": [
    { "resource": "Agent" },
    { "actor": "Workspaces" }
  ],
  "duration": 30
}
```

### Get Webhook Interest Registration

**GET** `/telephony/webhookInterestRegistrations`

Returns the current webhook interest registration.

#### Response Example

```json
{
  "interests": [
    { "resource": "Agent" },
    { "actor": "Workspaces" }
  ],
  "expiresAt": "2026-08-01T00:00:00.000Z"
}
```

### Delete Webhook Interest Registration

**DELETE** `/telephony/webhookInterestRegistrations`

Deletes the webhook interest registration.

### Interest Types

#### Resource-based Interests

| **Value** | **Description** |
|-----------|-----------------|
| `Hook Status` | Enables webhook events for the `telephony_hookstatus` resource. |
| `Agent` | Enables webhook events for the `telephony_agent` resource. |
| `Services` | Enables webhook events for the `telephony_services` resource. |
| `Agent Monitoring` | Enables webhook events for the `telephony_agentMonitoring` resource. |
| `Queue` | Enables webhook events for the `telephony_queue` resource. |
| `Queue Monitoring` | Enables webhook events for the `telephony_queueMonitoring` resource. |

#### Actor-based Interests

| **Value** | **Description** |
|-----------|-----------------|
| `Workspaces` | Enables telephony webhook events associated with workspace actors. |
| `Virtual Lines` | Enables telephony webhook events associated with virtual line actors. |

---

## Use Case: Call Queue Performance Metrics

This example walks through building an application to extract an organization's call queue performance metrics.

### Step 1: Identify Required APIs

- List call queues in the organization
- Register for `telephony_queueMonitoring` webhooks

### Step 2: Create a Service App

Identify the required scopes:

- `spark-admin:telephony_config_read` — to read call queues
- `spark-admin:calls_read` — to register `telephony_queueMonitoring` webhooks

Create the Service App with these scopes. You can start using it in your own organization without publishing to the App Hub.

### Step 3: Authorize the Service App

1. As an organization administrator, authorize the Service App in Control Hub
2. Retrieve the access and refresh tokens for the authorizing organization

### Step 4: Enumerate Organization Content

Use the [Read the List of Call Queue or Customer Assist Queues](https://developer.webex.com/docs/api/v1/features-call-queue/read-the-list-of-call-queue-or-customer-assist-queues) API to list all call queues.

### Step 5: Set Up WebHooks

1. **Register webhook callback:** Use the Webhooks API to register an org-level webhook for `telephony_queueMonitoring`
2. **Register interest:** Use the interest registration API to register interest for `telephony_queueMonitoring`
3. **Set up refresh:** Create a periodic task to refresh interest registrations before they expire

### Step 6: Receive WebHooks

On webhook reception, extract:

- `actorId` — corresponds to the call queue ID
- Performance metrics from `monitoringStatus`: `averageHandlingTime`, `expectedWaitTime`, `averageSpeedOfAnswer`, `longestWaitTime`, `numCallsInQueue`, `numAgentsAssigned`, `numAgentsStaffed`, `numStaffedAgentsIdle`, `numStaffedAgentsUnavailable`

### Step 7: Correlate Data

Match the queue ID from the webhook with queue details from enumeration to display queue names alongside performance metrics.

### Step 8: Publish the Service App

When ready, submit the Service App for publication on the Webex App Hub. Once published, any organization administrator can authorize it.

<a id="webhook-payload-schemas"></a>

## Webhook Payload Schemas

This section provides detailed schema information for each telephony webhook resource.

### Common Webhook Envelope Fields

All telephony webhook payloads share a common envelope structure:

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `id` | string | A unique identifier for the webhook. |
| `name` | string | A user-friendly name for the webhook. |
| `targetUrl` | string | The URL that receives the webhook. |
| `resource` | string | The resource type for the webhook (e.g., `telephony_calls`, `telephony_agent`). |
| `event` | string | Event type: `created`, `updated`, or `deleted`. |
| `orgId` | string | The organization that owns the webhook. |
| `createdBy` | string | The ID of the entity that added the webhook. |
| `appId` | string | The ID of the Webex app that was used to create the webhook. |
| `ownedBy` | string | Indicates if the webhook is owned by the `org` or the `creator`. |
| `status` | string | Status of the webhook. Always `active` for emitted webhooks. |
| `created` | string | Date and time the webhook was created. |
| `actorId` | string | The unique identifier of the entity who caused the webhook to be sent. |
| `data` | object | The event-specific payload (see resource schemas below). |

### Common Telephony Payload Fields

All telephony webhook `data` payloads include:

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventTimestamp` | string | Date and time the event was emitted (ISO 8601 format). |
| `actorType` | string | The type of the actor: `PEOPLE`, `PLACE`, `VIRTUAL_LINE`, or `CALL_QUEUE`. |
| `eventType` | string | The specific event type (varies by resource). |

---

### telephony_calls

Notification of calls progression through each state.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `originating` | An outgoing call is being originated |
| `originated` | An outgoing call has been originated |
| `received` | An incoming call was received |
| `answered` | The call was answered |
| `held` | The call was placed on hold |
| `resumed` | The call was resumed from hold |
| `recordingStarting` | Call recording is starting |
| `recordingStarted` | Call recording has started |
| `recordingPaused` | Call recording was paused |
| `recordingResumed` | Call recording was resumed |
| `recordingStopped` | Call recording was stopped |
| `disconnected` | The call was disconnected |
| `transferred` | The call was transferred |
| `bargedIn` | The call was barged into |
| `retrieved` | The call was retrieved |
| `pickedUp` | The call was picked up |
| `forwarded` | The call was forwarded |
| `updated` | The call was updated |

#### Call Data Fields

| **Field** | **Type** | **Required** | **Description** |
|-----------|----------|--------------|-----------------|
| `callId` | string | Yes | The call identifier of the call. |
| `callSessionId` | string | Yes | The call session identifier. Can be used to correlate multiple calls in the same session. |
| `personality` | string | Yes | The personality of the call: `originator`, `terminator`, or `clickToDial`. |
| `state` | string | Yes | Current state: `connecting`, `alerting`, `connected`, `held`, `remoteHeld`, or `disconnected`. |
| `remoteParty` | object | Yes | The remote party's details (see <a href="#party-information">Party Information</a>). |
| `created` | string | Yes | The date and time the call was created. |
| `muteCapable` | boolean | Yes | Indicates whether the call supports mute/unmute APIs. |
| `muted` | boolean | Yes | Indicates whether the call is currently muted. |
| `appearance` | integer | No | The appearance value for the call (for ordering on devices). |
| `answered` | string | No | The date and time the call was answered. |
| `disconnected` | string | No | The date and time the call was disconnected. |
| `redirections` | array | No | List of previous redirections (see <a href="#redirection-information">Redirection Information</a>). |
| `recall` | object | No | Recall details for incoming calls (e.g., park recall). |
| `recordingState` | string | No | Recording state: `pending`, `started`, `paused`, `stopped`, or `failed`. |
| `completedElsewhere` | boolean | No | Indicates if the call was completed elsewhere. |
| `parkedAgainstParty` | object | No | Details of the party against which this call is parked (see <a href="#party-information">Party Information</a>). |
| `executiveId` | string | No | The ID of the Executive for Executive Assistant service. |
| `allowedRecordingControls` | array | No | Recording controls allowed: `record`, `pause`, `stop`, `resume`. |
| `endpointId` | string | No | The ID of the endpoint linked to the call. |
| `endpointType` | string | No | Endpoint type: `CALLING_DEVICE`, `APPLICATION`, or `HOTDESKING_GUEST`. |
| `networkEndpointNumber` | string | No | The address of the network endpoint linked to the call. |
| `networkEndpointType` | string | No | Network endpoint type: `EXECUTIVE_ASSISTANT` or `SINGLE_NUMBER_REACH`. |

#### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_calls",
  "event": "created",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "creator",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "received",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtODkxMjU0MTQ6MA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "personality": "terminator",
    "state": "alerting",
    "muteCapable": false,
    "muted": false,
    "remoteParty": {
      "name": "Espace Commun",
      "number": "888",
      "placeId": "Y2lzY29zcGFyazovL3VzL1BMQUNFLzcxMTVjNjYyLTY2NmYtNDEwMS1iMjUzLTU4OGVkMTIzNTk0MA",
      "id": "Y2lzY29zcGFyazovL3VzL1BMQUNFLzcxMTVjNjYyLTY2NmYtNDEwMS1iMjUzLTU4OGVkMTIzNTk0MA",
      "idType": "PLACE",
      "privacyEnabled": false,
      "callType": "location"
    },
    "appearance": 1,
    "created": "2026-01-07T22:11:00.018Z",
    "completedElsewhere": false,
    "endpointId": "Y2lzY29zcGFyazovL3VzL0NBTExJTkdfREVWSUNFLzJjMzEyNGM4LWM1OWEtNDgwMC1iYmI1LTU5NDM4ZjUwMGZhNA",
    "endpointType": "CALLING_DEVICE"
  }
}
```

---

### telephony_agent

Notification of call queue agent changes.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `join` | The agent has joined or left a queue |
| `state` | The agent's state has changed |
| `code` | The agent has entered wrap-up codes |

#### Event: join

Notification with the information on the call queue the agent is joining or leaving.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `join` for this event. |
| `joinInfo` | array | Array of queue join information objects. |

##### Join Info Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueId` | string | The queue ID. |
| `hasCxEssentials` | boolean | Denotes if the call queue has Customer Experience Essentials license. |
| `queueAutoAnswer` | boolean | Denotes if calls routed from a Customer Assist call queue to an available agent are answered automatically. |
| `allowLogoff` | boolean | Denotes if the agent is allowed to log on/off from the queue. |
| `status` | string | Join status: `joined`, `unjoined`, or `unassigned`. |
| `skillLevel` | integer | Skill level of the agent (for Skill-Based Routing queues). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agent",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "join",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "joinInfo": [
      {
        "queueId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
        "hasCxEssentials": true,
        "queueAutoAnswer": true,
        "allowLogoff": true,
        "status": "joined",
        "skillLevel": 12
      }
    ]
  }
}
```

#### Event: state

Notification when a call queue agent state changes.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `state` for this event. |
| `acdStateInfo` | object | Agent state information object (see <a href="#acd-state-info-object">ACD State Info Object</a>). |

<a id="acd-state-info-object"></a>

##### ACD State Info Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `state` | string | Current state: `signIn`, `available`, `unavailable`, `wrapUp`, or `signOut`. |
| `stateModifiedBy` | string | Entity that triggered the change: `agent`, `supervisor`, `admin`, or `policy`. |
| `supervisorId` | string | The supervisor that triggered the state change (if applicable). |
| `policyReason` | string | Policy reason: `unreachable`, `no-answer`, `busy`, `other`, or `wrap-up`. |
| `wrapUpDetails` | object | Additional details when entering wrap-up state (see <a href="#wrap-up-details">Wrap-Up Details</a>). |
| `stateTimestamp` | string | Timestamp of the last agent state change. |
| `signinTimestamp` | string | Timestamp of the agent sign-in. |
| `totalAvailableTime` | integer | Total available time since last sign-in. |
| `averageWrapUpTime` | object | Average wrap-up time per handled call. Contains `value` field. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agent",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "state",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "acdStateInfo": {
      "state": "unavailable",
      "stateModifiedBy": "policy",
      "supervisorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9iNTlhMWY5NS1kMzMwLTRmMDEtYWUyNy1jNGM3M2I0YmVhYjE=",
      "policyReason": "wrap-up",
      "wrapUpDetails": {
        "queueId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
        "queueName": "cx_essential_name",
        "queueNumber": "+15146977514",
        "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
        "wrapUpChangeId": "WrapUpChange_id_01",
        "maxWrapUpEndTime": "2024-09-10T01:19:22.903Z",
        "remoteParty": {
          "name": "Espace Commun",
          "number": "888",
          "id": "Y2lzY29zcGFyazovL3VzL1BMQUNFLzcxMTVjNjYyLTY2NmYtNDEwMS1iMjUzLTU4OGVkMTIzNTk0MA",
          "idType": "PLACE",
          "privacyEnabled": false,
          "callType": "location"
        }
      },
      "stateTimestamp": "2023-09-13T15:19:08.280Z",
      "signinTimestamp": "2023-09-13T12:10:21.432Z",
      "totalAvailableTime": 0,
      "averageWrapUpTime": {
        "value": 10
      }
    }
  }
}
```

#### Event: code

Notification when a call queue agent enters a wrap-up code.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `code` for this event. |
| `wrapUpCodes` | array | Array of wrap-up code strings to tag the call with. |
| `callId` | string | Identifier of the call to tag. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agent",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "code",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "wrapUpCodes": ["Promotion", "Customer Follow-up"],
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtODkxMjU0MTQ6MA"
  }
}
```

---

### telephony_agentMonitoring

Notification of call queue agent performance metrics.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `updated` | Agent monitoring status has been updated |

#### Agent Monitoring Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `eventType` | string | Always `updated` for this payload. |
| `monitoringStatus` | object | Agent monitoring status object (see <a href="#agent-monitoring-status-object">Agent Monitoring Status Object</a>). |

<a id="agent-monitoring-status-object"></a>

##### Agent Monitoring Status Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `averageACDCallTime` | object | Average call time for call queue calls since last sign-in. Contains `value` field. |
| `averageACDOutgoingCallTime` | object | Average call time for outgoing call queue calls since last sign-in. Contains `value` field. |

#### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_agentMonitoring",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "data": {
    "actorType": "PEOPLE",
    "eventType": "updated",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "monitoringStatus": {
      "averageACDCallTime": {
        "value": 6154
      },
      "averageACDOutgoingCallTime": {
        "value": 0
      }
    }
  }
}
```

---

### telephony_queue

Notification of call queue calls progression.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `callAbandoned` | A call is abandoned by the caller and removed from the queue |
| `callAdded` | A call is added to the queue |
| `callAnsweredByAgent` | A call has been answered by an agent and removed from the queue |
| `callBounced` | A call is bounced back to the queue after being offered to an agent |
| `callEscaped` | The caller dials the configured escape digits while in the queue |
| `callForwarded` | The forced forwarding policy is triggered for a call |
| `callForwardedTreatmentCompleted` | The announcement is completed for a call treated according to the Forced Forwarding policy |
| `callOfferedToAgent` | A call is offered to an agent. The call remains in the queue until answered |
| `callOverflowed` | The overflow policy is triggered for a call in the queue |
| `callOverflowedTreatmentCompleted` | The announcement is completed for a call treated according to the Overflow policy |
| `callPromoted` | A call has been promoted to a different priority in the queue |
| `callReleased` | A call is released from the queue |
| `callReordered` | A call is reordered within the queue |
| `callStranded` | A call is identified as stranded and removed from the queue |
| `callStrandedTreatmentCompleted` | The announcement is completed for a call treated according to the Stranded call policy |
| `callStrandedUnavailable` | A call is identified as stranded due to agent unavailability |
| `callStrandedUnavailableTreatmentCompleted` | The announcement is completed for a call treated according to the Stranded - Unavailable call policy |
| `callTransferred` | A call is transferred to a new destination and removed from the queue |
| `callUpdated` | The remote party attributes are modified while the call is in the queue |
| `holidayPolicyApplied` | The Holiday policy is triggered for a call |
| `holidayPolicyTreatmentCompleted` | The announcement is completed for a call treated according to the Holiday policy |
| `nightPolicyApplied` | The Night policy is triggered for a call |
| `nightPolicyTreatmentCompleted` | The announcement is completed for a call treated according to the Night policy |
| `whisperStarted` | An agent answers an offered call and the whisper announcement is started |

<a id="common-queue-entry-object"></a>

#### Common Queue Entry Object

Most queue events include a `queueEntry` object with the following fields:

| **Field** | **Type** | **Description** |
|-----------|----------|------------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue (DNIS). |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `origCallId` | string | The original call ID for the queue entry. Only present when the queue entry's call ID has changed due to a scenario such as callback where a new call replaces the original call. |
| `addTime` | string | The time when this entry was added to the queue. |
| `removeTime` | string | The time when this entry was removed from the queue. |
| `priority` | string | Priority: `highest`, `high`, `medium`, or `low`. Only present for premium call centers. |
| `bounced` | boolean | Present and true when the call has been bounced one or more times. |
| `reordered` | boolean | Present and true when the call has been reordered within the queue. |
| `mandatoryEntrance` | boolean | Present and true when the call is being played the mandatory entrance message. |
| `preservedWaitTime` | integer | The total time in milliseconds spent waiting in previous queue(s) when transferred. Only present when applicable. |
| `addTimeInPriorityBucket` | string | The time this entry was added to the priority bucket in the queue. |
| `preservedWaitTimeInPriorityBucket` | integer | The preserved wait time in milliseconds this entry has accumulated when being inserted in the priority bucket. Only present when applicable. |
| `answeringAgentId` | string | The ID of the agent that answered the call. Only present when the call is answered. |
| `answeringAgentType` | string | Type of agent: `PEOPLE`, `PLACE`, or `VIRTUAL_LINE`. Only present when the call is answered. |
| `answeringCallId` | string | The call ID of the agent call when answered. Only present for non-distributed calls. |
| `answeringNetworkCallId` | string | The SIP call ID of the agent call when answered. Only present for distributed calls where the call offer from the call queue to the agent contains a SIP call leg. |

#### Event: callAbandoned

Notification when a call has been abandoned by a remote party while in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `entrancePlaying` | boolean | True if the entrance message was playing when the call was abandoned. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callAbandoned",
    "eventTimestamp": "2010-04-19T21:09:53.257Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTMxOTc6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T21:08:15.635Z",
      "removeTime": "2010-04-19T21:09:53.257Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest",
      "bounced": true
    }
  }
}
```

#### Event: callAdded

Notification when a new call is added to the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `position` | integer | The position of the call in the queue. |
| `redirections` | array | Array of redirection information (see <a href="#redirection-information">Redirection Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callAdded",
    "eventTimestamp": "2010-04-19T20:59:21.291Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTMxNDk6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T20:59:21.291Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "position": 1
  }
}
```

#### Event: callAnsweredByAgent

Notification when a call has been answered by an agent and removed from the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information including `answeringAgentId`, `answeringAgentType`, and `answeringCallId` or `answeringNetworkCallId` (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callAnsweredByAgent",
    "eventTimestamp": "2026-04-27T14:24:03.563Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtMjA0MDQxNDY5MDY6MA",
      "callSessionId": "ZjNkODI0ODEtYWU3OS00NjgxLTk1YjYtMmZjNzk1MjI5MDNk",
      "queueName": "Q-ME-Operator",
      "queueNumber": "59821",
      "addTime": "2026-04-27T14:23:56.646Z",
      "removeTime": "2026-04-27T14:24:03.563Z",
      "remoteParty": {
        "name": "ARC3 GASES",
        "number": "+12524463257",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    }
  }
}
```

#### Event: callBounced

Notification when a call is bounced back to the queue after being offered to an agent.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information with `bounced` set to true (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `position` | integer | The new position of the call in the queue (if reordered). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callBounced",
    "eventTimestamp": "2010-04-19T21:08:15.635Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTMxOTc6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T21:08:15.635Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest",
      "bounced": true
    }
  }
}
```

#### Event: callEscaped

Notification when the caller dials the configured escape digits while in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callEscaped",
    "eventTimestamp": "2010-04-20T15:04:07.356Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTk2NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_2_Name",
      "queueNumber": "+15006001027",
      "addTime": "2010-04-20T14:55:55.321Z",
      "removeTime": "2010-04-20T15:04:07.356Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest",
      "reordered": true
    }
  }
}
```

#### Event: callForwarded

Notification when the forced forwarding policy is triggered for a call.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |
| `redirections` | array | Array of redirection information (see <a href="#redirection-information">Redirection Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callForwarded",
    "eventTimestamp": "2010-04-21T20:25:08.100Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNzg5MzM6MA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "ACD_CTI1_Name",
    "queueNumber": "+15006001025",
    "remoteParty": {
      "name": "NetworkN1FirstName NetworkN1LastName",
      "number": "+15007003333",
      "privacyEnabled": false,
      "callType": "external"
    },
    "redirect": {
      "destination": "1011",
      "reason": "divert",
      "redirectTime": "2010-04-21T20:25:08.100Z"
    }
  }
}
```

#### Event: callOfferedToAgent

Notification when a call is offered to an agent. The call remains in the queue until answered.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callOfferedToAgent",
    "eventTimestamp": "2010-04-19T20:59:21.291Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTMxNDk6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T20:59:21.291Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    }
  }
}
```

#### Event: callOverflowed

Notification when the overflow policy is triggered for a call in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `overflowReason` | string | Reason for overflow (see <a href="#overflow-reason-enum">Overflow Reason Enum</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |
| `redirections` | array | Array of redirection information (see <a href="#redirection-information">Redirection Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callOverflowed",
    "eventTimestamp": "2010-04-19T21:30:12.671Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQwMjU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T21:29:42.671Z",
      "removeTime": "2010-04-19T21:30:12.671Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "overflowReason": "time",
    "redirect": {
      "destination": "1026",
      "reason": "divert",
      "redirectTime": "2010-04-19T21:30:12.671Z"
    }
  }
}
```

#### Event: callPromoted

Notification when a call has been promoted to a different priority in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information with updated priority (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `position` | integer | The new position of the call in the queue. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callPromoted",
    "eventTimestamp": "2010-04-20T14:56:26.140Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTk2NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_2_Name",
      "queueNumber": "+15006001027",
      "addTime": "2010-04-20T14:55:55.321Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "position": 2
  }
}
```

#### Event: callReleased

Notification when a call is released from the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callReleased",
    "eventTimestamp": "2010-12-14T19:06:06.976Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtMTI5OjA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-12-14T19:04:53.018Z",
      "removeTime": "2010-12-14T19:06:06.976Z",
      "remoteParty": {
        "name": "callcenter callcenter",
        "number": "+15146987610",
        "privacyEnabled": false,
        "callType": "location"
      },
      "priority": "highest"
    }
  }
}
```

#### Event: callReordered

Notification when a call is reordered within the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information with `reordered` set to true (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `position` | integer | The new position of the call in the queue. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callReordered",
    "eventTimestamp": "2010-04-20T14:56:26.140Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTk2NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_2_Name",
      "queueNumber": "+15006001027",
      "addTime": "2010-04-20T14:55:55.321Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest",
      "reordered": true
    },
    "position": 1
  }
}
```

#### Event: callStranded

Notification when a call is identified as stranded and removed from the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |
| `redirections` | array | Array of redirection information (see <a href="#redirection-information">Redirection Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callStranded",
    "eventTimestamp": "2010-04-20T00:23:47.613Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQ1NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T00:23:36.743Z",
      "removeTime": "2010-04-20T00:23:47.613Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    }
  }
}
```

#### Event: callStrandedUnavailable

Notification when a call is identified as stranded due to agent unavailability. The call is removed from the queue and handled per the Stranded Calls - Unavailable routing policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callStrandedUnavailable",
    "eventTimestamp": "2010-04-20T00:23:47.613Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQ1NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T00:23:36.743Z",
      "removeTime": "2010-04-20T00:23:47.613Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    }
  }
}
```

#### Event: callTransferred

Notification when a call is transferred to a new destination and removed from the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `redirect` | object | Redirect details for the transfer destination (see <a href="#redirect-information">Redirect Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callTransferred",
    "eventTimestamp": "2010-04-20T13:16:16.187Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTgyMjU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T13:15:44.207Z",
      "removeTime": "2010-04-20T13:16:16.187Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "redirect": {
      "destination": "6001011",
      "reason": "divert",
      "redirectTime": "2010-04-20T13:16:16.187Z"
    }
  }
}
```

#### Event: callUpdated

Notification when the remote party attributes are modified while the call is in the queue.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information with updated remote party details (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `reason` | string | Update reason (see <a href="#call-update-reason-enum">Call Update Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callUpdated",
    "eventTimestamp": "2010-04-20T13:26:05.048Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTgzNjU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T13:26:05.048Z",
      "remoteParty": {
        "number": "+17003334",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "reason": "Call Transferred"
  }
}
```

#### Event: whisperStarted

Notification when an agent answers an offered call and the whisper announcement is started.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "whisperStarted",
    "eventTimestamp": "2010-04-19T20:59:21.291Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTMxNDk6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T20:59:21.291Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest",
      "answeringAgentId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hZ2VudEExQGJyb2Fkc29mdC5jb20",
      "answeringAgentType": "PEOPLE",
      "answeringCallId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTMxNTM6MA"
    }
  }
}
```

#### Event: holidayPolicyApplied

Notification when the Holiday policy is triggered for a call.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |
| `redirections` | array | Array of redirection information (see <a href="#redirection-information">Redirection Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "holidayPolicyApplied",
    "eventTimestamp": "2010-04-23T15:12:10.325Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNzkyOTc6MA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "ACD_CTI1_Name",
    "queueNumber": "+15006001025",
    "remoteParty": {
      "name": "NetworkN1FirstName NetworkN1LastName",
      "number": "+15007003333",
      "privacyEnabled": false,
      "callType": "external"
    },
    "redirect": {
      "destination": "1011",
      "reason": "divert",
      "redirectTime": "2010-04-23T15:12:10.325Z"
    }
  }
}
```

#### Event: nightPolicyApplied

Notification when the Night policy is triggered for a call.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `treatmentStarted` | boolean | True if treatment announcement has started. |
| `redirections` | array | Array of redirection information (see <a href="#redirection-information">Redirection Information</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "nightPolicyApplied",
    "eventTimestamp": "2010-04-23T15:12:10.325Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtMjcxOjA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "callcenter",
    "queueNumber": "+15146987610",
    "remoteParty": {
      "name": "john3 south",
      "number": "+15146987603",
      "privacyEnabled": false,
      "callType": "location"
    }
  }
}
```

#### Event: callForwardedTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Forced Forwarding policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callForwardedTreatmentCompleted",
    "eventTimestamp": "2010-04-21T20:25:08.100Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNzg5MzM6MA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "ACD_CTI1_Name",
    "queueNumber": "+15006001025",
    "remoteParty": {
      "name": "NetworkN1FirstName NetworkN1LastName",
      "number": "+15007003333",
      "privacyEnabled": false,
      "callType": "external"
    },
    "redirect": {
      "destination": "1011",
      "reason": "divert",
      "redirectTime": "2010-04-21T20:25:08.100Z"
    },
    "reason": "EOF"
  }
}
```

#### Event: callOverflowedTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Overflow policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `overflowReason` | string | Reason for overflow (see <a href="#overflow-reason-enum">Overflow Reason Enum</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callOverflowedTreatmentCompleted",
    "eventTimestamp": "2010-04-19T21:30:12.671Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQwMjU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-19T21:29:42.671Z",
      "removeTime": "2010-04-19T21:30:12.671Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "overflowReason": "time",
    "redirect": {
      "destination": "1026",
      "reason": "divert",
      "redirectTime": "2010-04-19T21:30:12.671Z"
    },
    "reason": "EOF"
  }
}
```

#### Event: callStrandedTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Stranded call policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callStrandedTreatmentCompleted",
    "eventTimestamp": "2010-04-20T00:23:47.613Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQ1NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T00:23:36.743Z",
      "removeTime": "2010-04-20T00:23:47.613Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "reason": "EOF"
  }
}
```

#### Event: callStrandedUnavailableTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Stranded - Unavailable call policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueEntry` | object | Queue entry information (see <a href="#common-queue-entry-object">Common Queue Entry Object</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "callStrandedUnavailableTreatmentCompleted",
    "eventTimestamp": "2010-04-20T00:23:47.613Z",
    "queueEntry": {
      "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNTQ1NDU6MA",
      "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
      "queueName": "ACD_CTI1_Name",
      "queueNumber": "+15006001025",
      "addTime": "2010-04-20T00:23:36.743Z",
      "removeTime": "2010-04-20T00:23:47.613Z",
      "remoteParty": {
        "name": "NetworkN1FirstName NetworkN1LastName",
        "number": "+15007003333",
        "privacyEnabled": false,
        "callType": "external"
      },
      "priority": "highest"
    },
    "reason": "remoteRelease"
  }
}
```

#### Event: holidayPolicyTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Holiday policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "holidayPolicyTreatmentCompleted",
    "eventTimestamp": "2010-04-23T15:12:10.325Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtNzkyOTc6MA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "ACD_CTI1_Name",
    "queueNumber": "+15006001025",
    "remoteParty": {
      "name": "NetworkN1FirstName NetworkN1LastName",
      "number": "+15007003333",
      "privacyEnabled": false,
      "callType": "external"
    },
    "redirect": {
      "destination": "1011",
      "reason": "divert",
      "redirectTime": "2010-04-23T15:12:10.325Z"
    },
    "reason": "EOF"
  }
}
```

#### Event: nightPolicyTreatmentCompleted

Notification when the announcement is completed for a call treated according to the Night policy.

##### Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `callId` | string | The call identifier. |
| `callSessionId` | string | The call session identifier. |
| `queueName` | string | The name of the call queue. |
| `queueNumber` | string | The phone number of the call queue. |
| `remoteParty` | object | Information about the remote party (see <a href="#party-information">Party Information</a>). |
| `redirect` | object | Redirect details (see <a href="#redirect-information">Redirect Information</a>). |
| `reason` | string | Treatment completion reason (see <a href="#treatment-completion-reason-enum">Treatment Completion Reason Enum</a>). |

##### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svYmQzMWFjNzYtMWVjMS00ZTIwLTg1ZDMtNDRiNWM2Yjk2ODU5",
  "name": "My Awesome Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queue",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85NmIwODlkOS0wZmQ4LTRlNzQtOWI3Ni01MGRhZjc2ODcwNWM",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0NmMzkyNWU5NDFmMzhhYTc0M2Y0MmFiNzcwZmZhZjFhNTIyMjcxZDI5OTQ4NDhjNjk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "org",
  "status": "active",
  "created": "2026-01-07T22:10:44.031Z",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvMzM1Yzk1NzgtZjA0NS00NzgzLTgwYWEtMWNiY2Q2MjZhOTEx",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "nightPolicyTreatmentCompleted",
    "eventTimestamp": "2010-04-23T15:12:10.325Z",
    "callId": "Y2lzY29zcGFyazovL3VzL0NBTEwvY2FsbGhhbGYtMjcxOjA",
    "callSessionId": "Njk1YjEzNjktNzQxZi00MzgwLTljMTEtNzI2ODE0YTE3MDZj",
    "queueName": "callcenter",
    "queueNumber": "+15146987610",
    "remoteParty": {
      "name": "john3 south",
      "number": "+15146987603",
      "privacyEnabled": false,
      "callType": "location"
    },
    "reason": "EOF"
  }
}
```

---

### telephony_queueMonitoring

Notification of call queue performance metrics.

#### Event Types

| **eventType** | **Description** |
|---------------|-----------------|
| `updated` | Queue monitoring status has been updated |

#### Queue Monitoring Payload Fields

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `actorType` | string | Always `CALL_QUEUE` for this resource. |
| `eventType` | string | Always `updated` for this payload. |
| `queueName` | string | The name of the call queue. |
| `monitoringStatus` | object | Queue monitoring status object. |

##### Queue Monitoring Status Object

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `averageHandlingTime` | object | Average handling time for calls to this queue. Contains `value` field. |
| `expectedWaitTime` | object | Expected wait time for calls. Not present if no agents in Available or Wrap-Up state. Contains `value` field. |
| `averageSpeedOfAnswer` | object | Average speed of answer for calls. Contains `value` field. |
| `longestWaitTime` | object | Longest wait time of any calls in the queue. Contains `value` field. |
| `numCallsInQueue` | object | Number of calls in the queue. Contains `value` field. |
| `numAgentsAssigned` | integer | Number of agents assigned to the queue. |
| `numAgentsStaffed` | integer | Number of agents staffing the queue. |
| `numStaffedAgentsIdle` | integer | Number of staffed agents that are idle (not on a call and in available state). |
| `numStaffedAgentsUnavailable` | integer | Number of staffed agents in the unavailable state. |

#### Example Payload

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svOTg3NjU0MzItYWJjZC0xMjM0LWVmZ2gtMTIzNDU2Nzg5MGFi",
  "name": "My Queue Monitoring Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "telephony_queueMonitoring",
  "event": "updated",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi9mMTMxNjFlNC04N2Q5LTQ4MDAtYmJiNS01OTQzOGY1MDBmYTQ",
  "ownedBy": "org",
  "status": "active",
  "actorId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjMTIzZGVmNDU2",
  "data": {
    "actorType": "CALL_QUEUE",
    "eventType": "updated",
    "eventTimestamp": "2026-01-07T22:11:00.023Z",
    "queueName": "Support Queue",
    "monitoringStatus": {
      "averageHandlingTime": {
        "value": 180
      },
      "expectedWaitTime": {
        "value": 45
      },
      "averageSpeedOfAnswer": {
        "value": 30
      },
      "longestWaitTime": {
        "value": 120
      },
      "numCallsInQueue": {
        "value": 5
      },
      "numAgentsAssigned": 10,
      "numAgentsStaffed": 8,
      "numStaffedAgentsIdle": 3,
      "numStaffedAgentsUnavailable": 2
    }
  }
}
```

---

## Common Schema Objects

<a id="party-information"></a>

### Party Information

Information about a call party (caller or callee).

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `name` | string | The party's name. Only present when available and privacy is not enabled. |
| `number` | string | The party's number (digits or URI). Only present when available and privacy is not enabled. |
| `personId` | string | The party's person ID. Only present for Webex users when privacy is not enabled. |
| `placeId` | string | The party's place ID. Only present for workspaces when privacy is not enabled. |
| `virtualLineId` | string | The party's virtual line ID. Only present for virtual lines when privacy is not enabled. |
| `id` | string | The party's ID. Only present when available and privacy is not enabled. |
| `idType` | string | Type of ID: `PEOPLE`, `PLACE`, or `VIRTUAL_LINE`. |
| `privacyEnabled` | boolean | Indicates whether privacy is enabled for name, number, and IDs. |
| `callType` | string | Call type: `location`, `organization`, `external`, `emergency`, `repair`, or `other`. |

<a id="redirection-information"></a>

### Redirection Information

Information about a call redirection.

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `reason` | string | Redirection reason: `busy`, `noAnswer`, `unavailable`, `unconditional`, `timeOfDay`, `divert`, `followMe`, `huntGroup`, `callQueue`, or `unknown`. |
| `redirectingParty` | object | Details of the party who redirected the call (see <a href="#party-information">Party Information</a>). |

<a id="redirect-information"></a>

### Redirect Information

Information about a redirect action.

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `destination` | string | The destination for the redirect (digits or URI). |
| `reason` | string | The reason for the redirect. |
| `redirectTime` | string | The time at which the redirect took place. |

<a id="wrap-up-details"></a>

### Wrap-Up Details

Additional details when an agent enters wrap-up state.

| **Field** | **Type** | **Description** |
|-----------|----------|-----------------|
| `queueId` | string | The queue ID the call was received on. |
| `queueName` | string | The queue name the call was received on. |
| `queueNumber` | string | The queue number the call was received on. |
| `callSessionId` | string | The call session identifier. |
| `wrapUpChangeId` | string | An arbitrary string that changes when the list of available wrap-up codes changes. |
| `maxWrapUpEndTime` | string | The timestamp for max end time for wrap-up. |
| `remoteParty` | object | The details of the party calling the call queue (see <a href="#party-information">Party Information</a>). |

<a id="call-update-reason-enum"></a>

### Call Update Reason Enum

Reasons for a `callUpdated` event in the queue.

| **Value** | **Description** |
|-----------|-----------------|
| `Call Transferred` | The call was transferred. |
| `Call Picked-Up` | The call was picked up. |
| `Call Barged-In` | The call was barged into. |
| `Call Monitored` | The call was monitored. |
| `Call Forwarded` | The call was forwarded. |
| `Call Park Retrieved` | The call was retrieved from park. |
| `Unknown` | The reason is unknown. |

<a id="overflow-reason-enum"></a>

### Overflow Reason Enum

Reasons for a `callOverflowed` event.

| **Value** | **Description** |
|-----------|-----------------|
| `size` | The queue overflowed due to reaching maximum size. |
| `time` | The queue overflowed due to maximum wait time being exceeded. |

<a id="treatment-completion-reason-enum"></a>

### Treatment Completion Reason Enum

Reasons for treatment completion events (e.g., `callForwardedTreatmentCompleted`, `holidayPolicyTreatmentCompleted`).

| **Value** | **Description** |
|-----------|-----------------|
| `EOF` | The treatment announcement completed normally (end of file). |
| `remoteRelease` | The remote party released the call before the treatment completed. |

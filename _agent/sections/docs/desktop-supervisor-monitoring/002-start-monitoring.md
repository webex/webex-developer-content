---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-supervisor-monitoring
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Monitoring Module
- Start Monitoring
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-supervisor-monitoring). [Full Markdown](../../../../docs/desktop-supervisor-monitoring.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Use the Desktop SDK to monitor active calls and manage supervisor monitoring events.

## Parent context

## Call Monitoring Module

Call monitoring enables supervisors to monitor agents who are engaged in active calls with customers.

## Selected section

### Start Monitoring

The `Desktop.monitoring.startMonitoring` request monitors the calls received by an agent.

**Example**

```javascript
  Desktop.monitoring.startMonitoring({
      id: "62e5ffa9-7d80-40d7-bfbc-94cab8d5f67b", // Unique monitoring request identifier
      monitorType: "adhoc", // adhoc, continuous, midcall
      trackingId: "62e5ffa9-7d80-40d7-bfbc-94cab8d5f67b", // string
      taskId: "d6583397-d7ab-4dcb-b761-6cc925ad11d4" // string – nothing but interaction id
    });
```

**Parameters**

| Name        | Type   | Description                                   | Required |
| ----------- | ------ | --------------------------------------------- | -------- |
| id          | String | Unique identifier for the monitoring request. | Yes      |
| monitorType | String | Monitoring type: `adhoc`, `continuous`, or `midcall`. | Yes |
| taskId | String | Unique identifier for the task. | Yes |
| trackingId | String | Unique identifier for the monitoring request that maps success and failure events. | Yes |

#### Start Monitoring Success

After initiating the startMonitoring request, the listener listens to the `eMonitoringOffered` event when the call monitoring is successful.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eMonitoringOffered", (msg) =>
      console.log("Monitoring eMonitoringOffered: ", msg)
);
```

**Example Response**

```json
{
  "data": {
    "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
    "id": "faedfcc8-035a-41e3-ad53-ee9fad4ca286",
    "monitorType": "adhoc",
    "supervisorId": "ae3dfcc8-035a-41e3-ad53-ee9fad4ca286",
    "queueId": "AXk4lbZds49yBk2m_M0b",
    "queueName": "Some Queue",
    "supervisorDN": "+14085550001",
    "taskId": "eeed32bd-19aa-4da0-8bee-e413d1799f4c",
    "task":{
       "callAssociatedData":{
          "DispositionCode":{
             "agentEditable":true,
             "displayName":"Disposition Code",
             "name":"DispositionCode",
             "type":"STRING",
             "value":"Please Enter Disposition"
          },
          "Some_Site":{
             "agentEditable":false,
             "displayName":"Location Called",
             "name":"Some_Site",
             "type":"STRING",
             "value":"Some Services"
          },
          "ani":{
             "agentEditable":false,
             "displayName":"ani",
                    "name":"ani",
             "type":"STRING",
             "value":"**********"
          },
          "dn":{
             "agentEditable":false,
             "displayName":"dn",
             "name":"dn",
             "type":"STRING",
             "value":"**********"
          },
          "ronaTimeout":{
             "agentEditable":false,
             "displayName":"ronaTimeout",
             "name":"ronaTimeout",
             "type":"STRING",
             "value":"18"
          },
          "virtualTeamName":{
             "agentEditable":false,
             "displayName":"virtualTeamName",
             "name":"virtualTeamName",
             "type":"STRING",
             "value":"Sample Marketing LAA"
          }
       },
       "callAssociatedDetails":{
          "ani":"+191****1028",
          "dn":"+191****2118",
          "ronaTimeout":"18",
          "virtualTeamName":"Some Marketing"
       },
       "callFlowParams":{

       },
       "callProcessingDetails":{
          "CONTINUE_RECORDING_ON_TRANSFER":"true",
          "EP_ID":"AXjrWErNWmiYcFh7QDSQ",
          "QMgrName":"aqm",
          "QueueId":"AXk4lbZds49y881m_M0b",
          "ani":"+191****1028",
          "dnis":"+191****2118",
          "fceRegisteredEvents":"",
          "isParked":"false",
          "mohFileName":"defaultmusic_on_hold.wav",
          "pauseDuration":"0",
          "pauseResumeEnabled":"false",
          "priority":"10",
          "recordInProgress":"true",
          "recordingStarted":"true",
          "ronaTimeout":"18",
          "routingStrategyId":"AXjv16JJJ3z7afsera2j",
          "taskToBeSelfServiced":"false",
          "tenantId":"285",
          "virtualTeamName":"Some Marketing",
          "vteamId":"AXk4lbZds49y771m_M0b",
          "workflowId":"607eee3242312e179b59e02b",
          "workflowName":"Sample work flow"
       },
       "contactDirection":{
          "type":"INBOUND"
       },
       "currentVTeam":"AXk4lbZds49yBk2m_M0b",
       "interactionId":"761c2d42-5b40-4dd4-a888-ae7c82f9ae94",
       "isFcManaged":true,
       "isTerminated":false,
       "media":{
          "761c2d42-5b40-4fd4-a888-aeff82f9ae94":{
             "holdTimestamp":null,
             "isHold":false,
             "mType":"mainCall",
             "mediaMgr":"vmm",
             "mediaResourceId":"761c2ff2-5b40-4fd4-a888-ae7c82f9ae94",
             "mediaType":"telephony",
             "participants":[
                "**********",
                "17eb03c9-2eae-4ce0-822b-cfff4b30239a"
             ]
          }
       },
       "mediaChannel":"broadcloud",
       "mediaType":"telephony",
       "orgId":"5b02f5ac-b2a3-4219-8a66-ca1cff83bd17",
       "outboundType":null,
       "owner":"17eb03c9-2eae-4ce0-822b-cfd1ff30239a",
       "participants":{
          "**********":{
             "id":"**********",
             "pType":"Customer",
             "type":"Customer"
          },
          "17eb03c9-2eae-4ce0-822b-cfd14bff239a":{
             "channelId":"fd8d3fee-0b75-4fff-b1c3-eceb2f1d9f98",
             "consultState":null,
             "consultTimestamp":null,
             "dn":"916***8420",
             "hasJoined":true,
             "id":"17eff3c9-2eae-4ce0-822b-cfd14b30239a",
             "isConsulted":false,
             "isWrapUp":false,
             "joinTimestamp":1238879263354,
             "lastUpdated":1624379263354,
             "name":"First Last Name",
             "pType":"Agent",
             "queueId":"AXk4lbZds4ddBk1m_M0b",
             "queueMgrId":"aqm",
             "sessionId":"d2d52b14-dd1e-4796-befc-288003425977",
             "siteId":"526",
             "teamId":"9336",
             "teamName":"Marketing",
             "type":"Agent",
             "wrapUpTimestamp":null
          }
       },
       "previousVTeams":[
          "AXjrWErNWmiYcDh7QQCQ"
       ],
       "queuedTimestamp":null,
       "state":"connected",
       "workflowManager":null
    },
    "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
    "type": "MonitoringOffered",
    "eventType": "SupervisorDesktopMessage"
  },
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
```

#### Start Monitoring Create Failed

If the start monitoring request fails, the listener listens to the `eMonitoringRequestCreateFailed` event.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eMonitoringRequestCreateFailed", (msg) =>
      console.log("Monitoring eMonitoringRequestCreateFailed: ", msg)
    );
```

**Example Response**

```json
{
  "data": {
    "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
    "id": "faedfcc8-035a-41e3-ad53-ee9fad4ca286",
    "monitorType": "adhoc",
    "supervisorId": "ae3dfcc8-035a-41e3-ad53-ee9fad4ca286",
    "queueId": ["AXk4lbZds49yBk2m_M0b", "AXk4lbZ23449yBk2m_M0b"],
    "teams": ["All"],
    "sites": ["All"],
    "agents": ["All"],
    "isActive": true,
    "taskId": null,
    "reason": "Supervisor already have a matching monitoring request",
    "reasonCode": 12345,
    "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
    "type": "MonitoringRequestCreateFailed",
    "eventType": "SupervisorDesktopMessage"
  },
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
```

#### Start Monitoring Call Offer Event to Supervisor

If the supervisor accepts a call on a physical device, the listener listens to the `eMonitoringStarted` event.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eMonitoringStarted", (msg) =>
      console.log("Monitoring eMonitoringStarted: ", msg)
    );
```

**Example Response**

```json
{
  "data": {
    "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
    "id": "faedfcc8-035a-41e3-ad53-ee9fad4ca286",
    "monitorType": "midcall",
    "supervisorId": "ae3dfcc8-035a-41e3-ad53-ee9fad4ca286",
    "queueId": "AXk4lbZds49yBk2m_M0b",
    "queueName": "Some Queue",
    "supervisorDN": "+14085550001",
    "taskId": "eeed32bd-19aa-4da0-8bee-e413d1799f4c",
    "task":{
       "callAssociatedData":{
          "DispositionCode":{
             "agentEditable":true,
             "displayName":"Disposition Code",
             "name":"DispositionCode",
             "type":"STRING",
             "value":"Please Enter Disposition"
          },
          "Some_Site":{
             "agentEditable":false,
             "displayName":"Location Called",
             "name":"Some_Site",
             "type":"STRING",
             "value":"Some Services"
          },
          "ani":{
             "agentEditable":false,
             "displayName":"ani",
             "name":"ani",
             "type":"STRING",
             "value":"**********"
          },
          "dn":{
             "agentEditable":false,
             "displayName":"dn",
             "name":"dn",
             "type":"STRING",
             "value":"**********"
          },
          "ronaTimeout":{
             "agentEditable":false,
             "displayName":"ronaTimeout",
             "name":"ronaTimeout",
             "type":"STRING",
             "value":"18"
          },
          "virtualTeamName":{
             "agentEditable":false,
             "displayName":"virtualTeamName",
             "name":"virtualTeamName",
             "type":"STRING",
             "value":"Sample Marketing LAA"
          }
       },
       "callAssociatedDetails":{
          "ani":"+191****1028",
          "dn":"+191****2118",
          "ronaTimeout":"18",
          "virtualTeamName":"Some Marketing"
       },
       "callFlowParams":{

       },
       "callProcessingDetails":{
          "CONTINUE_RECORDING_ON_TRANSFER":"true",
          "EP_ID":"AXjrWErNWmiYcFh7QDSQ",
          "QMgrName":"aqm",
          "QueueId":"AXk4lbZds49y881m_M0b",
          "ani":"+191****1028",
          "dnis":"+191****2118",
          "fceRegisteredEvents":"",
          "isParked":"false",
          "mohFileName":"defaultmusic_on_hold.wav",
          "pauseDuration":"0",
          "pauseResumeEnabled":"false",
          "priority":"10",
          "recordInProgress":"true",
          "recordingStarted":"true",
          "ronaTimeout":"18",
          "routingStrategyId":"AXjv16JJJ3z7afsera2j",
          "taskToBeSelfServiced":"false",
          "tenantId":"285",
          "virtualTeamName":"Some Marketing",
          "vteamId":"AXk4lbZds49y771m_M0b",
          "workflowId":"607eee3242312e179b59e02b",
          "workflowName":"Sample work flow"
       },
       "contactDirection":{
          "type":"INBOUND"
       },
       "currentVTeam":"AXk4lbZds49yBk2m_M0b",
       "interactionId":"761c2d42-5b40-4dd4-a888-ae7c82f9ae94",
       "isFcManaged":true,
       "isTerminated":false,
       "media":{
          "761c2d42-5b40-4fd4-a888-aeff82f9ae94":{
             "holdTimestamp":null,
             "isHold":false,
             "mType":"mainCall",
             "mediaMgr":"vmm",
             "mediaResourceId":"761c2ff2-5b40-4fd4-a888-ae7c82f9ae94",
             "mediaType":"telephony",
             "participants":[
                "**********",
                "17eb03c9-2eae-4ce0-822b-cfff4b30239a"
             ]
          }
       },
       "mediaChannel":"broadcloud",
       "mediaType":"telephony",
       "orgId":"5b02f5ac-b2a3-4219-8a66-ca1cff83bd17",
       "outboundType":null,
       "owner":"17eb03c9-2eae-4ce0-822b-cfd1ff30239a",
       "participants":{
          "**********":{
             "id":"**********",
             "pType":"Customer",
             "type":"Customer"
          },
          "17eb03c9-2eae-4ce0-822b-cfd14bff239a":{
             "channelId":"fd8d3fee-0b75-4fff-b1c3-eceb2f1d9f98",
             "consultState":null,
             "consultTimestamp":null,
             "dn":"916***8420",
             "hasJoined":true,
             "id":"17eff3c9-2eae-4ce0-822b-cfd14b30239a",
             "isConsulted":false,
             "isWrapUp":false,
             "joinTimestamp":1238879263354,
             "lastUpdated":1624379263354,
             "name":"First Last Name",
             "pType":"Agent",
             "queueId":"AXk4lbZds4ddBk1m_M0b",
             "queueMgrId":"aqm",
             "sessionId":"d2d52b14-dd1e-4796-befc-288003425977",
             "siteId":"526",
             "teamId":"9336",
             "teamName":"Marketing",
             "type":"Agent",
             "wrapUpTimestamp":null
          }
       },
       "previousVTeams":[
          "AXjrWErNWmiYcDh7QQCQ"
       ],
       "queuedTimestamp":null,
       "state":"connected",
       "workflowManager":null
    },
    "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
    "type": "MonitoringOffered",
    "eventType": "SupervisorDesktopMessage"
  },
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
```

#### Start Monitoring Call Failed

If call monitoring fails due to any reason, the listener listens to the `eMonitoringFailed` event.

**Example**

```javascript
    Desktop.monitoring.addEventListener("eMonitoringFailed", (msg) =>
      console.log("Monitoring eMonitoringFailed: ", msg)
    );
```

**Example Response**

````
{
  "data": {
    "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
    "id": "faedfcc8-035a-41e3-ad53-ee9fad4ca286",
    "monitorType": "midcall",
    "supervisorId": "ae3dfcc8-035a-41e3-ad53-ee9fad4ca286",
    "queueId": "AXk4lbZds49yBk2m_M0b",
    "queueName": "Some Queue",
    "supervisorDN": "+14085550001",
    "taskId": "eeed32bd-19aa-4da0-8bee-e413d1799f4c",
    "reason": "Supervisor (```Supervisor full name```) device is unresponsive",
    "reasonCode": 987562,
    "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
    "type": "MonitoringFailed",
    "eventType": "SupervisorDesktopMessage"
  },
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
````

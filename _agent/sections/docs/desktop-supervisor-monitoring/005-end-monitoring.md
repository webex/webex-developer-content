---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-supervisor-monitoring
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Monitoring Module
- End Monitoring
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

### End Monitoring

The `Desktop.monitoring.endMonitoring` request ends active call monitoring requests.

**Example**

```javascript
await Desktop.monitoring.endMonitoring ({ interactionId: "d6583397-d7ab-4dcb-b761-6cc925ad11d4" });
```

**Parameters**

| Name          | Type   | Description                           | Required |
| ------------- | ------ | ------------------------------------- | -------- |
| interactionId | String | Unique identifier of the interaction. | Yes      |

#### End Monitoring Success Event

After initiating the pause monitoring request to AQM, the listener listens to the `eMonitoringEnded` event.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eMonitoringEnded", (msg) =>
      console.log("Monitoring eMonitoringEnded: ", msg)
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
    "taskId": "eeed32bd-19aa-4da0-8bee-e413d1799f4c",
    "agentId": "ffddfcc8-035a-41e3-ad53-ee9fad4ca286",
    "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
    "type": "MonitoringEnded",
    "eventType": "SupervisorDesktopMessage"
  },
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
```

#### End Monitoring Failed Event

If End Monitoring fails, the `eMonitoringEndFailed` payload is delivered asynchronously.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eMonitoringEndFailed", (msg) =>
      console.log("Monitoring eMonitoringEndFailed: ", msg)
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
    "taskId": "eeed32bd-19aa-4da0-8bee-e413d1799f4c",
    "agentId": "ffddfcc8-035a-41e3-ad53-ee9fad4ca286",
    "reason": "Media leg failure",
    "reasonCode": 95367,
    "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
    "type": "MonitoringEndFailed",
    "eventType": "SupervisorDesktopMessage"
  },
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
```

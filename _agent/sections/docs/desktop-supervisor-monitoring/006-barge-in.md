---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-supervisor-monitoring
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Monitoring Module
- Barge In
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

### Barge In

The `Desktop.monitoring.bargeIn` request allows a supervisor to barge into an ongoing call between an agent and a customer, that is already being monitored.

**Example**

```javascript
await Desktop.monitoring.bargeIn ({ interactionId: "d6583397-d7ab-4dcb-b761-6cc925ad11d4" });
```

**Parameters**

| Name          | Type   | Description                           | Required |
| ------------- | ------ | ------------------------------------- | -------- |
| interactionId | String | Unique identifier of the interaction. | Yes      |

#### Barge In Success Event

After initiating the barge in request to AQM, the listener listens to the `eAgentMonitorStateChanged` event.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eAgentMonitorStateChanged", (msg) =>
      console.log("Monitoring eMonitoringEnded: ", msg)
    );
```

**Example Response**

```json
{
    "data": {
        "agentId": "6fc77132-5886-467f-b977-5b147770a7a7",
        "eventTime": 1693216938773,
        "eventType": "SupervisorDesktopMessage",
        "interactionId": "47ee78e5-a46c-446b-b607-8345d3f6c38d",
        "interaction":{},
        "monitoringState": {
            "type": "BargeIn"
        },
        "orgId": "c1040014-0ee0-4e9e-aaaf-e2bd54174760",
        "supervisorId": "075031e0-8013-4ae6-b59b-399a1b6ed19d",
        "supervisorName": "Intg Supervisor1",
        "trackingId": "f0d51000-17e1-4a38-a571-59e3b95ffa7e",
        "type": "AgentMonitorStateChanged"
    },
    "orgId": "c1040014-0ee0-4e9e-aaaf-e2bd54174760",
    "trackingId": "notifs_12a93135-7b69-4dd2-891c-df3096a5c437",
    "type": "AgentMonitorStateChanged"
}
```

#### Barge In Failed Event

If Barge In fails, the `eAgentMonitorStateChangeFailed` payload is delivered asynchronously.

**Example**

```javascript
  Desktop.monitoring.addEventListener("eAgentMonitorStateChangeFailed", (msg) =>
      console.log("Monitoring eAgentMonitorStateChangeFailed: ", msg)
    );
```

**Example Response**

```json
{
  "data": {
        "agentId": "6fc77132-5886-467f-b977-5b147770a7a7",
        "eventTime": 1693216938773,
        "eventType": "SupervisorDesktopMessage",
        "interactionId": "47ee78e5-a46c-446b-b607-8345d3f6c38d",
        "monitoringState": {
            "type": "BargeIn"
        },
        "orgId": "c1040014-0ee0-4e9e-aaaf-e2bd54174760",
        "supervisorId": "075031e0-8013-4ae6-b59b-399a1b6ed19d",
        "reason": "Media leg failure",
        "reasonCode": 95367,
        "trackingId": "46187830-fdd4-11eb-af48-410293f4b9ad",
        "type": "AgentMonitorStateChangeFailed"},
  "orgId": "f2ed32bd-19aa-4da0-8bee-e413d1799f4c",
  "trackingId": "notifs_e221605d-7806-4530-9e02-999cd5aae06a",
  "type": "MonitoringRequest"
}
```

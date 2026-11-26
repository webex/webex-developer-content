---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-outbound-callbacks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Schedule Callback Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-outbound-callbacks). [Full Markdown](../../../../docs/desktop-outbound-callbacks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Initiate outbound calls, update call-associated data, and manage scheduled callbacks with the Desktop SDK.

## Selected section

## Schedule Callback Module

The `Desktop.scheduleCallback` module provides methods to manage scheduled callbacks, including fetching, creating, updating, and deleting scheduled callback entries for agents.

**Example**

The `Desktop.scheduleCallback` module provides `fetchByAssigneeAgentId`, `fetchByCallbackPhoneNumber`, `createScheduleCallback`, `updateCallBackDetails`, `deleteScheduleCallback`, and `getValidCampaignTimes`. The sections below show the required arguments for each method.

### Methods

#### fetchByAssigneeAgentId(data)

Fetches scheduled callbacks for a given assignee agent ID. Returns a paginated list of scheduled callbacks assigned to the specified agent.

**Example**

```javascript
const result = await Desktop.scheduleCallback.fetchByAssigneeAgentId({
  data: {
    page: 0,
    assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    sortBy: "scheduledTime",
    sortOrder: "desc"
  }
});
```

**Parameters**

| Name           | Type   | Description                                                                 | Required |
| -------------- | ------ | --------------------------------------------------------------------------- | -------- |
| data           | Object | Options for fetching scheduled callbacks.                                   | Yes      |
| -->page        | Number | Page number for pagination (0-indexed).                                     | Yes      |
| -->assigneeAgent | String | Unique identifier of the assignee agent.                                  | Yes      |
| -->sortBy      | String | Field to sort results by (e.g., "scheduledTime").                           | No       |
| -->sortOrder   | String | Sort order direction. Possible values: "asc", "desc".                       | No       |

**Returns**

`{Object}` The object containing a `data` array of scheduled callbacks and a `meta` object with pagination information.

**Example Response**

```javascript
const fetchByAssigneeAgentIdResponse = {
  data: [
    {
      id: "4a86a573-4c5c-41f5-8970-a562488030d7",
      callbackOrigin: "api",
      createdTimestamp: "2026-01-28T10:30:00.000Z",
      lastUpdatedTimestamp: "2026-01-28T10:30:00.000Z",
      customerName: "John Doe",
      callbackNumber: "1234567890",
      timezone: "Asia/Calcutta",
      scheduleDate: "2026-02-01",
      startTime: "10:00:00",
      endTime: "11:00:00",
      assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
      queueId: "3cc44ceb-8287-4004-934d-ceaefeb170ad",
      callbackReason: "Follow-up call"
    }
    // ... more callbacks
  ],
  meta: {
    orgId: "12345678-abcd-efgh-ijkl-mnopqrstuvwx",
    page: 0,
    pageSize: 100,
    totalPages: 1,
    totalRecords: 1,
    links: {
      self: "/v1/callbacks/organization/.../scheduled-callback?..."
    }
  }
};
```

#### fetchByCallbackPhoneNumber(data)

Fetches scheduled callbacks for a given callback phone number. Returns a paginated list of scheduled callbacks matching the specified phone number.

**Example**

```javascript
const result = await Desktop.scheduleCallback.fetchByCallbackPhoneNumber({
  data: {
    page: 0,
    phoneNumber: "1234567890"
  }
});
```

**Parameters**

| Name           | Type   | Description                                                                 | Required |
| -------------- | ------ | --------------------------------------------------------------------------- | -------- |
| data           | Object | Options for fetching scheduled callbacks.                                   | Yes      |
| -->page        | Number | Page number for pagination (0-indexed).                                     | Yes      |
| -->phoneNumber | String | The callback phone number to search for.                                    | Yes      |

**Returns**

`{Object}` The object containing a `data` array of scheduled callbacks and a `meta` object with pagination information.
**Example Response**

```javascript
const fetchByCallbackPhoneNumberResponse = {
  data: [
    {
      id: "8c4e2f1a-3b5d-4e7f-9a1c-6d8e2f4a5b3c",
      callbackOrigin: "api",
      createdTimestamp: "2026-01-28T10:30:00.000Z",
      lastUpdatedTimestamp: "2026-01-28T10:30:00.000Z",
      customerName: "Jane Smith",
      callbackNumber: "1234567890",
      timezone: "America/New_York",
      scheduleDate: "2026-02-05",
      startTime: "14:00:00",
      endTime: "15:00:00",
      queueId: "c3d4e5f6-a7b8-4c9d-0e1f-2a3b4c5d6e7f",
      callbackReason: "Product inquiry"
    }
    // ... more callbacks
  ],
  meta: {
    orgId: "12345678-abcd-efgh-ijkl-mnopqrstuvwx",
    page: 0,
    pageSize: 100,
    totalPages: 1,
    totalRecords: 1,
    links: {
      self: "/v1/callbacks/organization/.../scheduled-callback?..."
    }
  }
};
```

#### createScheduleCallback(data)

Creates a new scheduled callback entry. This method allows agents to schedule callbacks for customers with specified time windows and optional agent assignment.

**Example**

```javascript
const result = await Desktop.scheduleCallback.createScheduleCallback({
  data: {
    callbackNumber: "1234567890",
    customerName: "Customer Name",
    timezone: "Asia/Calcutta",
    scheduleDate: "2026-01-01",
    startTime: "10:00:00",
    endTime: "11:00:00",
    assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    queueId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    callbackReason: "Callback Reason"
  }
});
```

**Parameters**

| Name              | Type   | Description                                                                                      | Required |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------ | -------- |
| data              | Object | Options for creating a scheduled callback.                                                       | Yes      |
| -->callbackNumber | String | The phone number to call back.                                                                   | Yes      |
| -->customerName   | String | Name of the customer for non-campaign callback.                                                   | No       |
| -->campaignId     | String | Unique identifier of the campaign; used for campaign callback.                                    | No       |
| -->timezone       | String | Timezone for the scheduled callback (e.g., "Asia/Calcutta", "America/New_York").                 | Yes      |
| -->scheduleDate   | String | Date for the scheduled callback in YYYY-MM-DD format.                                            | Yes      |
| -->startTime      | String | Start time of the callback window in HH:MM:SS format.                                            | Yes      |
| -->endTime        | String | End time of the callback window in HH:MM:SS format.                                              | Yes      |
| -->assigneeAgent  | String | Unique identifier of the agent to assign the callback.                                           | No       |
| -->queueId        | String | Unique identifier of the queue for the callback.                                                 | Yes      |
| -->callbackReason | String | Reason for the callback.                                                                         | Yes      |
| -->sourceInteraction | String | Source interaction id. This is the interaction id of the interaction that triggered the callback. | No       |

**Returns**

`{Object}` The created scheduled callback object.

**Example Response**

```javascript
const createScheduleCallbackResponse = {
  id: "c89cd57d-79f8-4fc7-b2ec-06aeb4684017",
  customerName: "Customer Name",
  callbackNumber: "1234567890",
  timezone: "Asia/Calcutta",
  scheduleDate: "2026-01-01",
  startTime: "10:00:00",
  endTime: "11:00:00",
  queueId: "2533784e-a89d-452e-baab-b5fb0c5fa0d7",
  callbackReason: "Callback Reason",
  sourceInteraction: null,
  callbackOrigin: "api",
  createdTimestamp: 1738231200000,
  lastUpdatedTimestamp: 1738231200000,
  assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
  assignedTime: 1738231199000,
  orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
  callbackType: "scheduled_personal"
};
```

#### updateCallBackDetails(data)

Updates an existing scheduled callback entry. All callback details can be modified except the callback ID.

**Example**

```javascript
const result = await Desktop.scheduleCallback.updateCallBackDetails({
  data: {
    id: "9f1e2d3c-4b5a-6c7d-8e9f-0a1b2c3d4e5f",
    callbackNumber: "1234567890",
    customerName: "Updated Customer Name",
    timezone: "Asia/Calcutta",
    scheduleDate: "2026-01-01",
    startTime: "10:00:00",
    endTime: "11:00:00",
    assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    queueId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    callbackReason: "Updated Callback Reason"
  }
});
```

**Parameters**

| Name              | Type   | Description                                                                                      | Required |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------ | -------- |
| data              | Object | Options for updating a scheduled callback.                                                       | Yes      |
| -->id             | String | Unique identifier of the scheduled callback to update.                                          | Yes      |
| -->callbackNumber | String | The phone number to call back.                                                                   | Yes      |
| -->customerName   | String | Name of the customer for non-campaign callback.                                                  | No       |
| -->campaignId     | String | Unique identifier of the campaign; used for campaign callback.                                   | No       |
| -->timezone       | String | Timezone for the scheduled callback (e.g., "Asia/Calcutta", "America/New_York").                 | Yes      |
| -->scheduleDate   | String | Date for the scheduled callback in YYYY-MM-DD format.                                            | Yes      |
| -->startTime      | String | Start time of the callback window in HH:MM:SS format.                                            | Yes      |
| -->endTime        | String | End time of the callback window in HH:MM:SS format.                                              | Yes      |
| -->assigneeAgent  | String | Unique identifier of the agent to assign the callback.                                           | No       |
| -->queueId        | String | Unique identifier of the queue for the callback.                                                 | Yes      |
| -->callbackReason | String | Reason for the callback.                                                                         | Yes      |

**Returns**

`{Object}` The updated scheduled callback object.

**Example Response**

```javascript
const updateCallBackDetailsResponse = {
  id: "c89cd57d-79f8-4fc7-b2ec-06aeb4684017",
  customerName: "Updated Customer Name",
  callbackNumber: "1234567890",
  timezone: "Asia/Calcutta",
  scheduleDate: "2026-01-01",
  startTime: "10:00:00",
  endTime: "11:00:00",
  queueId: "2533784e-a89d-452e-baab-b5fb0c5fa0d7",
  callbackReason: "Updated Callback Reason",
  sourceInteraction: null,
  callbackOrigin: "api",
  createdTimestamp: 1738231200000,
  lastUpdatedTimestamp: 1738234800000,
  assigneeAgent: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
  assignedTime: 1738231199000,
  orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
  callbackType: "scheduled_personal"
};
```

#### deleteScheduleCallback(data)

Deletes a scheduled callback entry by its unique identifier.

**Example**

```javascript
const result = await Desktop.scheduleCallback.deleteScheduleCallback({
  data: {
    id: "9f1e2d3c-4b5a-6c7d-8e9f-0a1b2c3d4e5f"
  }
});
```

**Parameters**

| Name   | Type   | Description                                                              | Required |
| ------ | ------ | ------------------------------------------------------------------------ | -------- |
| data   | Object | Options for deleting a scheduled callback.                               | Yes      |
| -->id  | String | Unique identifier (UUID) of the scheduled callback to delete.            | Yes      |

**Note:** The `id` parameter must be a valid UUID format.

#### getValidCampaignTimes(data)

Retrieves valid campaign callback time slots for a given campaign and agent. Use this method to get the campaign's weekly schedule and date overrides so that agents can schedule callbacks only within allowed time windows (for example, when creating a scheduled callback from a campaign interaction).

**Example**

```javascript
const result = await Desktop.scheduleCallback.getValidCampaignTimes({
  data: {
    campaignId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    interactionId: "f1e2d3c4-b5a6-4c7d-8e9f-0a1b2c3d4e5f"
  }
});
```

**Parameters**

| Name            | Type   | Description                                                                 | Required |
| --------------- | ------ | --------------------------------------------------------------------------- | -------- |
| data            | Object | Options for fetching valid campaign times.                                  | Yes      |
| -->campaignId   | String | Unique identifier of the campaign.                                          | Yes      |
| -->agentId      | String | Unique identifier of the agent.                                             | Yes      |
| -->interactionId | String | Unique identifier of the interaction that triggered the callback (e.g. the campaign call). Optional. | No       |

**Returns**

`{Object}` The object containing `data` with the campaign's valid time configuration: time zone, weekly schedule (per day), date overrides, and a success flag.

**Example Response**

```javascript
const getValidCampaignTimesResponse = {
  type: "CampaignValidTimesResponse",
  orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
  trackingId: "tracking-id-123",
  data: {
    type: "CampaignValidTimesResponse",
    agentId: "7d12d9ea-e8e0-41ee-81bf-c11a685b64ed",
    campaignId: "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    result: true,
    timeZone: "America/New_York",
    eventType: "CampaignValidTimesResponse",
    eventTime: 1738231200000,
    orgId: "58f1a59e-245c-4536-9ee4-06560658e493",
    trackingId: "tracking-id-123",
    weeklySchedule: {
      monday: [{ start: "09:00", end: "13:00" }, { start: "14:00", end: "18:00" }],
      tuesday: [{ start: "09:00", end: "17:00" }],
      wednesday: [{ start: "10:00", end: "14:00" }],
      thursday: [{ start: "09:00", end: "13:00" }, { start: "14:00", end: "18:00" }],
      friday: [{ start: "09:00", end: "12:00" }],
      saturday: [{ start: "10:00", end: "15:00" }],
      sunday: []
    },
    dateOverrides: [
      {
        date: "2026-01-15",
        shiftTimes: [{ start: "11:00", end: "16:00" }]
      }
    ]
  }
};
```

The `data.weeklySchedule` object has keys for each day of the week (`monday` through `sunday`). Each day's value is an array of time slots with `start` and `end` in `"HH:mm"` format. The `data.dateOverrides` array lists specific dates (YYYY-MM-DD) with custom shift times that override the weekly schedule. Use `data.result` to confirm the request succeeded; use `data.timeZone` when displaying or validating schedule times.

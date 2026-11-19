---
type: Guide
title: Web Calling SDK | Call History
display_title: Call History
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history)

This article explains the call history feature available in the calling SDK. 

---

The calling SDK consists of various modules which are created at the time of its initialization — `CallHistoryClient` is one of those modules designed to facilitate the retrieving, managing, and interacting with `callHistory` records.

Refer to the [Getting Started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how a `calling` instance is created and different modules are instantiated.

## Instantiating the CallHistoryClient

The `CallHistoryClient` is implemented as the `CallHistory` class in the SDK and there are two ways of instantiating it.

To instantiate just the `CallHistoryClient`, use the `createCallHistoryClient` method:

```javascript
const callHistory = createCallHistoryClient(webex, logger);
```

If the `CallHistoryClient` is initialized through the `calling` instantiation:

```javascript
const callHistory = calling.callHistory;
```

## Core Methods
This client provides APIs to fetch call history data, update missed calls status, and delete call history records.

### Fetch Call History

The `getCallHistoryData()` method retrieves the `callHistory` records for a user based on specified parameters.

```javascript
const callHistoryResponse = await callHistory.getCallHistoryData(  
  numberOfDays,  
  limit,  
  sort,  
  sortBy  
);
```

This method accepts folowing input parameters:

### Parameters

| **Name**      | **Description**                                              | **Values**                     | **Required** |
|---------------|--------------------------------------------------------------|--------------------------------|--------------|
| **days**      | Number of days to fetch the `callHistory` data               | `number` (default: `7`)        | No           |
| **limit**     | Number of records to be fetched                              | `number` (default: `50`)       | No           |
| **sort**      | Sort the records in `ascending` or `descending` order        | `string` (default: `DESC`)     | No           |
| **sortBy**    | Sort the records by `startTime` or `endTime`                 | `string` (default: `END_TIME`) | No           |

### Returns

Promise resolving to a `JanusResponseEvent` object with the following structure:
**Promise<[JanusResponseEvent](#janusresponseevent)>**

Here's an example of a response for the `getCallHistoryData()` method:

#### JanusResponseEvent

```javascript
{  
  statusCode: number;  
  data: {  
    userSessions: UserSession[];  
    error?: string;  
  };  
  message: string | null;  
}
```

#### UserSession

```javascript
{
  id: string;
  sessionId: string;
  disposition: Disposition;
  startTime: string;
  endTime: string;
  url: string;
  durationSeconds: number;
  joinedDurationSeconds: number;
  participantCount: number;
  isDeleted: boolean;
  isPMR: boolean;
  correlationIds: string[];
  links: {
    locusUrl?: string;
    conversationUrl?: string;
    callbackAddress: string;
  };
  self: {
    id: string;
    name?: string;
    phoneNumber?: string;
    cucmDN?: string;
    ucmLineNumber?: number;
  };
  durationSecs: number;
  other: {
    ownerId?: string;
    id: string;
    name?: string;
    sipUrl?: string;
    primaryDisplayString?: string;
    secondaryDisplayString?: string;
    isPrivate: boolean;
    callbackAddress: string;
    phoneNumber?: string;
    contact?: string;
    email?: string;
  };
  sessionType: 'SPARK' || 'WEBEXCALLING',;
  direction: string;
  callingSpecifics?: {
    redirectionDetails: {
      phoneNumber?: string;
      sipUrl?: string;
      name?: string;
      reason: string;
      userId?: string;
      isPrivate: boolean;
    };
  };
}
```

### Update Missed Calls

The `updateMissedCalls()` method updates the read state of user missed calls based on the specified parameters.

```javascript
const updateMissedCallsResponse = await callHistory.updateMissedCalls(endTimeSessionIds);
```

This method accepts the following input parameters:

### Parameters

| **Name**              |  **Description**                                                                           | **Values**         | **Required** |
|-----------------------|--------------------------------------------------------------------------------------------|--------------------|--------------|
| **endTimeSessionIds** | An array of objects containing `endTime` and `sessionId` of missed `callHistory` records.  | EndTimeSessionId[] | Yes          |

#### EndTimeSessionId

```javascript
[
  {
    "endTime": "2024-05-22T08:50:48.603Z",
    "sessionId": "d74d19cc-6aa7-f341-6012-aec433cc6f8d"
  }
]
```

### Returns
Promise resolving to an `UpdateMissedCallsResponse` object with the following structure:
**Promise<[UpdateMissedCallsResponse](#updatemissedcallsresponse)>**

Here's an example of a response for the `updateMissedCalls()` method:

#### UpdateMissedCallsResponse

```javascript
{
  statusCode: number;
  data: {
    readStatusMessage?: string;
    error?: string;
  };
  message: string | null;
}
```

### Delete Call History Records

The `deleteCallHistoryRecords()` method deletes `callHistory` records based on the specified parameters.

```javascript
const deleteCallHistoryRecordsResponse = await callHistory.deleteCallHistoryRecords(deleteSessionIds);
```

It accepts the following input parameters:

### Parameters
| **Name**             | **Description**                                                                                        | **Values**         | **Required** |
|----------------------|--------------------------------------------------------------------------------------------------------|--------------------|--------------|
| **deleteSessionIds** | An array of objects containing `endTime` and `sessionId` of the `callHistory` records to be deleted.   | EndTimeSessionId[] | Yes          |

The [`EndTimeSessionId`](#endtimesessionid) structure is the same as used in the `updateMissedCalls` method.

### Returns

Promise resolving to a `DeleteCallHistoryRecordsResponse` object with the following structure:
**Promise<[DeleteCallHistoryRecordsResponse](#deletecallhistoryrecordsresponse)>**

Here's an example of a response for the `deleteCallHistoryRecords()` method:

#### DeleteCallHistoryRecordsResponse

```javascript
{
  statusCode: number;
  data: {
    deleteStatusMessage?: string;
    error?: string;
  };
  message: string | null;
}
```

## Event Handling

The `CallHistoryClient` emits following events that you can listen for to receive real-time updates about `callHistory`.

### callHistory:user_recent_sessions

Emitted when new call history session data is available and received. Event payload is of type [CallSessionEvent](#callsessionevent).

#### CallSessionEvent

```javascript
{  
  id: string;  
  data: {  
    userSessions: {  
      userSessions: UserSession[];  
      statusCode: number;  
    };  
    eventType: string;  
  };  
  timestamp: number;  
  trackingId: string;  
}
```

### callHistory:user_viewed_sessions

Emitted when call history sessions are marked as viewed/read. Event payload is of type [CallSessionViewedEvent](#callsessionviewedevent).

#### CallSessionViewedEvent

```javascript
{  
  id: string;  
  data: {  
    userReadSessions: {  
      userReadSessions: UserReadSessions[];  
      statusCode: number;  
    };  
    eventType: string;  
  };  
  timestamp: number;  
  trackingId: string;  
}
```

### callHistory:user_sessions_deleted

Emitted when call history sessions are deleted. Event payload is of type [CallSessionDeletedEvent](#callsessiondeletedevent)

#### CallSessionDeletedEvent
```javascript
{  
  id: string;  
  data: {  
    deletedSessions: string[];  
    eventType: string;  
  };  
  timestamp: number;  
  trackingId: string;  
}
```

### Listen for Call History Events

You can subscribe to `callHistory` events using the on() method:

```javascript
callHistory.on('callHistory:user_recent_sessions', (sessionData: CallSessionEvent) => {  
  console.log('Users recent session data : ', sessionData.data.userSessions.userSessions[0]);  
});

callHistory.on('callHistory:user_viewed_sessions', (event: CallSessionViewedEvent) => {  
  console.log('User viewed sessions: ', event.data.userReadSessions.userReadSessions);  
}); 

callHistory.on('callHistory:user_sessions_deleted', (event: CallSessionDeletedEvent) => {  
  console.log('User deleted sessions: ', event.data.deletedSessions);  
});
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Core Methods
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-call-history.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article explains the call history feature available in the calling SDK. 

---

The calling SDK consists of various modules which are created at the time of its initialization — `CallHistoryClient` is one of those modules designed to facilitate the retrieving, managing, and interacting with `callHistory` records.

Refer to the [Getting Started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how a `calling` instance is created and different modules are instantiated.

## Selected section

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
**Promise<[JanusResponseEvent](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#janusresponseevent)>**

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
**Promise<[UpdateMissedCallsResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#updatemissedcallsresponse)>**

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

The [`EndTimeSessionId`](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#endtimesessionid) structure is the same as used in the `updateMissedCalls` method.

### Returns

Promise resolving to a `DeleteCallHistoryRecordsResponse` object with the following structure:
**Promise<[DeleteCallHistoryRecordsResponse](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#deletecallhistoryrecordsresponse)>**

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

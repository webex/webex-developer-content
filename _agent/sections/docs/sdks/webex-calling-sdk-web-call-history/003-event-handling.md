---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Event Handling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-call-history.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article explains the call history feature available in the calling SDK. 

---

The calling SDK consists of various modules which are created at the time of its initialization — `CallHistoryClient` is one of those modules designed to facilitate the retrieving, managing, and interacting with `callHistory` records.

Refer to the [Getting Started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how a `calling` instance is created and different modules are instantiated.

## Selected section

## Event Handling

The `CallHistoryClient` emits following events that you can listen for to receive real-time updates about `callHistory`.

### callHistory:user_recent_sessions

Emitted when new call history session data is available and received. Event payload is of type [CallSessionEvent](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#callsessionevent).

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

Emitted when call history sessions are marked as viewed/read. Event payload is of type [CallSessionViewedEvent](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#callsessionviewedevent).

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

Emitted when call history sessions are deleted. Event payload is of type [CallSessionDeletedEvent](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history#callsessiondeletedevent)

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

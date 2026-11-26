---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Meeting Widget changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](011-limitations.md)

## Article introduction

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Selected section

## Meeting Widget changes

Please adhere to the guidelines below to transition from utilizing `roomId/spaceId` to `meetingId/sipUrl` within the Meetings Widget.

### Before...

You'd use code like the following to create a Webex meeting widget using a specified room ID or space ID:

```javascript
import { WebexMeetingsWidget } from '@webex/widgets';

import '@webex/widgets/dist/css/webex-widgets.css';

export default function App() {
  return (
    <WebexMeetingsWidget
      style={{ width: '1000px', height: '500px' }} // Substitute with any arbitrary size or use `className`
      accessToken='<ACCESS_TOKEN>'
      meetingDestination='<ROOM_ID>' // NOTICE THIS LINE
    />
  );
}
```

### After...

1. Use **step-1** from [SDK Changes](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings#sdk-changes) to obtain `meetingId` or `sipUrl`.

2. The code snippet below illustrates the process of creating a Webex meeting using either a meeting ID or a SIP URL:

```javascript
import { WebexMeetingsWidget } from '@webex/widgets';

import '@webex/widgets/dist/css/webex-widgets.css';

export default function App() {
  return (
    <WebexMeetingsWidget
      style={{ width: '1000px', height: '500px' }} // Substitute with any arbitrary size or use `className`
      accessToken='<ACCESS_TOKEN>'
      meetingDestination='<MEETING_ID OR SIP_URL>' // NOTICE THIS LINE
    />
  );
}
```



> **Info**
>
> If `spaceId` is passed for `meetingDestination` the widget will throw an error.

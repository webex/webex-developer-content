---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Task APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

## Task APIs

The Task APIs allow agents to manage tasks effectively. These APIs provide the necessary controls to handle tasks.

### Basic Controls

Basic controls provide fundamental operations for managing tasks, such as accepting, declining, holding, resuming, and wrapping up tasks.

#### Accept Task

To accept an incoming task:

```js
const acceptResponse = await task.accept();
```

#### Decline Task

To decline an incoming task:

```js
const declineResponse = await task.decline();
```

#### Hold Task

To hold a task:

```js
const holdResponse = await task.hold();
```

#### Resume Task

To resume a task:

```js
const resumeResponse = await task.resume();
```

#### End Task

To end a task:

```js
const endResponse = await task.end();
```

#### Wrap Up Task

To wrap up a task:

```js
const wrapupPayload = {
  auxCodeId: `<AUX_CODE_ID>`, // Get from agentProfile.wrapupCodes
  wrapUpReason: `<WRAP_UP_REASON>` // Get from agentProfile.wrapupCodes
};
const wrapupResponse = await task.wrapup(wrapupPayload);
```

### Advanced Controls

Advanced controls provide additional functionality for managing tasks, such as pausing/resuming recordings, consulting and transferring tasks.

#### Pause Recording

To pause the call recording:

```js
const pauseRecordingResponse = await task.pauseRecording();
```

#### Resume Recording

To resume the call recording:

```js
// const resumeRecordingPayload = { ... }; // Define if needed
const resumeRecordingResponse = await task.resumeRecording(resumeRecordingPayload); // Pass payload if required
```

#### Consult Task

To consult a task:

```js
const consultPayload = {
  destination: 'myBuddyAgentId', // or queueId, entryPointId
  destinationType: 'AGENT', // or 'QUEUE', 'ENTRY_POINT'
  // mediaType: 'telephony' // if applicable
};
const consultResponse = await task.consult(consultPayload);
```

#### End Consult

To end a consult:

```js
const consultEndPayload = {
  // isConsult: true, // This parameter might be specific or implicit
  // queueId: 'myQueueId', // Include if transferring to queue post-consult
};
const endConsultResponse = await task.endConsult(consultEndPayload);
```

#### Transfer Task

To transfer a task:

```js
const transferPayload = {
  destination: 'myQueueId', // or agentId, entryPointId
  destinationType: 'QUEUE', // or 'AGENT', 'ENTRY_POINT'
  // mediaType: 'telephony' // if applicable
};
const transferResponse = await task.transfer(transferPayload);
```

#### Consult Transfer

To perform a consult transfer:

```js
const consultTransferPayload = {
  // destination: 'anotherAgentId', // Usually not needed if consult was established
  // destinationType: 'agent',
};
const consultTransferResponse = await task.consultTransfer(consultTransferPayload);
```

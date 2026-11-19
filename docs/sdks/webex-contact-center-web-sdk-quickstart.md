---
type: Guide
title: Webex Contact Center Web SDK | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart)

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Install the WxCC SDK

The WxCC SDK is available as a Node.js module via NPM. You can install it using either yarn or npm utilities:

To install the latest stable version of the Webex WxCC SDK, use npm:

```bash
npm install @webex/contact-center
```

Or, using yarn:

```bash
yarn add @webex/contact-center
```

### CDN

A minified version of the Webex WxCC SDK is also provided via [unpkg](//unpkg.com) and [jsdelivr](//jsdelivr.com) CDNs. To include the SDK via a CDN:

```html
<!-- unpkg -->
<script crossorigin src="https://unpkg.com/@webex/contact-center/umd/contact-center.min.js"></script>
<!-- jsdelivr -->
<script crossorigin src="https://cdn.jsdelivr.net/npm/@webex/contact-center/umd/contact-center.min.js"></script>
```

## Initialize the SDK

To create a new `Webex` object, replace `<AUTHORIZATION/BOT TOKEN>` below with your Personal Access Token.  
You can also control multi-session functionalities via the `allowMultiLogin` flag:

```js
import Webex from '@webex/contact-center'

const webex = Webex.init({
  credentials: {
    access_token: `<AUTHORIZATION/BOT TOKEN>`
  },
  config: {
    plugin: {
      allowMultiLogin: false
    }
  }
});

webex.once('ready', () => {
  console.log('Webex object is ready');
});
```

## Registration

You can only register the agent once the `webex` object is ready. You'll want to attach a listener for the `webex` object's `ready` event and proceed only after that event has fired:

```js
const agentProfile = await webex.cc.register();
// agentProfile is now available for use
```
When the subscription is successful, the `register` method returns a `Profile` object. This object contains details about the agent, such as their ID, name, and current state. This action enables the SDK to receive and handle events from the Contact Center backend, such as incoming tasks, state changes, and other agent-related events. The `Profile` is needed to identify and manage the agent within the Contact Center system.

## Agent Login

Before performing any actions, the agent must log in to the Webex Contact Center:

```js
const stationLoginResponse = await webex.cc.stationLogin({
  loginOption: 'BROWSER', // or 'EXTENSION', 'AGENT_DN'
  dialNumber: `<DIAL_NUMBER>`, // Required if loginOption is 'AGENT_DN' or 'EXTENSION'
  teamId: `<TEAM_ID>`
});
```

## Agent Logout

To logout the agent:

```js
const stationLogoutResponse = await webex.cc.stationLogout({ reason: 'End of shift' });
```

## Set Agent State

Agents can change their status using `setAgentState`:

```js
const agentStateResponse = await webex.cc.setAgentState({
  state: 'Available', // or 'Idle'
  auxCodeId: `<AUX_CODE_ID>`, // Required if state is 'Idle'
  lastStateChangeReason: `<REASON>`,
  // agentId: `<AGENT_ID>` // Typically not needed, SDK infers from context
});
```

To listen for agent state changes from other sources:

```js
webex.cc.on('agent:stateChange', (data) => {
  console.log('Agent state changed:', data);
});
```

## Handle Incoming Tasks

To listen for incoming calls or tasks:

```js
webex.cc.on('task:incoming', (task) => {
  console.log('Incoming task:', task);
  // Use the task object received in this event to call the task APIs
});

webex.cc.on('task:hydrate', (task) => {
  console.log('task:hydrate: ', task);
// This is used when a relogin or reload occurs while an active task is present.
});

webex.cc.on('task:assigned', (task) => {
  console.info('Task accepted: ', task.data.interactionId);
});
```

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

## Start an Outdial Call

Agents can initiate outbound calls using the following method:

```js
const outDialPayload = {
  entryPointId: `<CAMPAIGN_ID_OR_ENTRY_POINT_ID>`, // e.g., from agentProfile.outdialEntryPoints
  destination: `<DESTINATION_NUMBER>`, // Phone number to dial
  direction: 'OUTBOUND',
  mediaType: 'telephony',
  outboundType: 'OUTDIAL' // or 'CALLBACK'
};
const startOutdialResponse = await webex.cc.startOutdial(outDialPayload);
// A new task object for the outdial call will be emitted via 'task:incoming'.
```

## Get Buddy Agents

To get the list of buddy agents in the given state and media according to agent profile settings:

```js
const buddyAgentsData = {
  state: 'Available', // Optional: Filter by agent state (e.g., 'Available', 'Idle')
  mediaType: 'telephony' // Optional: Filter by media type
};
const buddyAgentsResponse = await webex.cc.getBuddyAgents(buddyAgentsData);
// buddyAgentsResponse contains an array of buddy agents.
```

## Station Re-login

To re-login the agent:

```js
const stationReLoginResponse = await webex.cc.stationReLogin();
```

## Complete Working Example

```html
<!DOCTYPE html>
<html>

<head>
  <title>Contact Center Agent</title>
  <script src="https://unpkg.com/webex@3.8.0-next.88/umd/webex.min.js"></script>
</head>

<body>
  <h1>Contact Center Agent</h1>

  <div>
    <input type="text" id="access-token"
      placeholder="Enter your access token">
    <button onclick="startAgent()">Start Agent</button>
  </div>

  <div id="status">Ready to start...</div>
  <button id="end-task-btn" onclick="endCurrentTask()" style="display: none;">End Task</button>
  <audio id="remote-audio" autoplay></audio>

  <script>
    let webex, agentProfile, deviceId, currentTask;

    async function startAgent() {
      const token = document.getElementById('access-token').value;
      const status = document.getElementById('status');

      try {
        // Initialize SDK
        status.textContent = 'Initializing SDK...';
        webex = Webex.init({
          credentials: { access_token: token }
        });

        await new Promise(resolve => webex.once('ready', resolve));

        // Register agent
        status.textContent = 'Registering agent...';
        agentProfile = await webex.cc.register();

        console.log('Agent Profile:', agentProfile);
        // Station login with error handling for existing session
        status.textContent = 'Logging into station...';
        try {
          const response = await webex.cc.stationLogin({
            teamId: agentProfile.teams[0].id,
            loginOption: 'BROWSER'
          });
          deviceId = response.deviceId;
        } catch (stationError) {
          if (stationError.message && stationError.message.includes('AGENT_SESSION_ALREADY_EXISTS')) {
            console.log('Agent session already exists, continuing to state change...');
            status.textContent = 'Agent session already active, setting state...';
          } else {
            throw stationError; // Re-throw if it's a different error
          }
        }

        // Set available
        status.textContent = 'Setting agent available...';
        await webex.cc.setAgentState({
          state: agentProfile.idleCodes[8].name,
          auxCodeId: agentProfile.idleCodes[8].id
        });

        // Handle tasks
        webex.cc.on('task:incoming', handleTask);
        webex.cc.on('task:hydrate', handleTask);

        status.textContent = 'Agent ready for tasks! 🎉';

      } catch (error) {
        status.textContent = 'Error: ' + error.message;
        console.error(error);
      }
    }

    async function handleTask(task) {
      const status = document.getElementById('status');
      console.log('New task:', task.data.interactionId);

      // Store current task
      currentTask = task;

      // Accept task
      await task.accept();
      status.textContent = 'Agent accepted the tasks! ';
      await new Promise(resolve => setTimeout(resolve, 5000));
      status.textContent = '5 second delay completed!';
      // Accept task
      await task.hold();
      status.textContent = 'Agent did hold the tasks! ';
      await new Promise(resolve => setTimeout(resolve, 5000));
      status.textContent = '5 second delay completed!';
      // Accept task
      await task.resume();
      status.textContent = 'Agent did resume the tasks! ';
      // Show end button after task is accepted
      document.getElementById('end-task-btn').style.display = 'inline-block';

      // Handle media for voice calls
      task.on('task:media', (track) => {
        document.getElementById('remote-audio').srcObject = new MediaStream([track]);
      });

      // Handle task end
      task.on('task:end', async (response) => {
        // Hide end button when task ends
        document.getElementById('end-task-btn').style.display = 'none';
        currentTask = null;
        status.textContent = 'Task ended: ' + response.data.interactionId;
        if (response.data.wrapUpRequired) {
          await task.wrapup({
            auxCodeId: agentProfile.wrapupCodes[0].id,
            wrapUpReason: agentProfile.wrapupCodes[0].name
          });
          status.textContent = 'Agent wrapup completed!';
        }
      });
    }

    async function endCurrentTask() {
      await currentTask.end();
    }
  </script>
</body>

</html>
```

## Troubleshooting

The Webex Contact Center SDK provides methods to upload logs for diagnosing and resolving issues. These logs include actions taken on the SDK such as login, logout and call handling, which can help Webex support troubleshoot SDK-related problems. The logs also include tracking and feedback IDs that can be shared with developer support to download the required logs remotely.

### Upload Logs

The `uploadLogs` method allows you to manually upload logs at any point during SDK usage. This is particularly useful when you encounter unexpected behavior or need to provide diagnostic information to Webex support.

#### Example Usage

```js
const uploadLogsResponse = await webex.cc.uploadLogs({ description: 'Optional issue description' });
// uploadLogsResponse.feedbackID contains the ID for the uploaded logs.
```

In addition to manual uploads, the SDK can automatically upload logs when certain errors occur. This ensures that critical diagnostic information is captured without requiring manual intervention. 

To expedite issue resolution, provide the following details to Webex support:

- **Correlation ID** or **feedbackID from the console logs/network requests** or 
- **User ID** with **Timestamp** of the error

These details help Webex support quickly locate the relevant logs and resolve the issue efficiently.

#### When to Use

- **Manual Uploads**: Use when you want to capture logs at a specific point in your application workflow.
- **Auto Uploads**: Logs are automatically uploaded during unexpected errors or failures. Users only need to provide the **Correlation ID**, **feedbackID** from console logs or network request/responses, or **User ID** with a **Timestamp** to Webex support for faster issue resolution.

By leveraging both manual and automatic log uploads, you can ensure comprehensive diagnostics and faster issue resolution.

## Summary

This guide covered the essential steps to get started with the Webex Contact Center SDK, including:
- Installing and initializing the SDK.
- Logging in an agent.
- Managing agent states.
- Handling incoming tasks.
- Logging out and making outbound calls.
- Fetching buddy agents.
- Re-logging in the agent.
- Accepting, declining, holding, resuming, ending, and wrapping up tasks.
- Pausing and resuming call recordings.
- Consulting and transferring tasks.
- Starting an outdial call.



> **Info**
>
> To support multi-session environments (e.g., multiple tabs or browsers), you must listen for agent and task events. For the full list, see the [Events reference](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-events).



For detailed API documentation, please refer to the [TypeDoc documentation](https://webex.github.io/webex-js-sdk/wxcc/).

Happy coding!

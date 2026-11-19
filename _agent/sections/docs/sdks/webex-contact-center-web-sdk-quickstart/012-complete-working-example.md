---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete Working Example
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

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

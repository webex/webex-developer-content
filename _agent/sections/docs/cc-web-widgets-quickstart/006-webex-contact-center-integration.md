---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Contact Center Integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-quickstart). [Full Markdown](../../../../docs/cc-web-widgets-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md) [Known Issues/Limitations](010-known-issues-limitations.md)

## Article introduction

This Quickstart Guide walks you through integrating Webex Contact Center capabilities using React widgets into your application from the ground up. Follow these steps to create a fully functional application.

## Selected section

## Webex Contact Center Integration

Follow these steps to get your integration up and running quickly.

1. Add the following code to the `App.jsx` file.

```js
import React, { useState, useEffect } from 'react';
import { StationLogin, UserState, IncomingTask, TaskList, CallControl, store, CallControlCAD } from '@webex/cc-widgets';
import { IconProvider, ThemeProvider } from '@momentum-design/components/dist/react';
import { observer } from 'mobx-react-lite';

import './App.css';

function App() {
  const [accessToken, setAccessToken] = useState('');
  const [isInitialized, setIsInitialized] = useState(false);
  const [isStationLogInSuccess, setIsStationLogInSuccess] = useState(false);
  const [incomingTasks, setIncomingTasks] = useState([]);

  useEffect(() => {
    // Set up incoming task callback
    store.setIncomingTaskCb(({ task }) => {
      console.log('Incoming task:', task);
      setIncomingTasks((prevTasks) => [...prevTasks, task]);
      playNotificationSound();
    });

    return () => {
      store.setIncomingTaskCb(undefined);
    };
  }, []);

  function playNotificationSound() {
    const ctx = new AudioContext();
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();

    // Use a waveform with richer harmonics, like 'triangle' or 'sawtooth'
    osc.type = 'triangle';
    osc.frequency.setValueAtTime(1200, ctx.currentTime); // High pitch for metal cling

    osc.connect(gain);
    gain.connect(ctx.destination);

    // Set the volume and create a quick decay to simulate the metallic sound
    gain.gain.setValueAtTime(0.5, ctx.currentTime); // Start loud
    gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.3); // Quick decay

    osc.start();
    osc.stop(ctx.currentTime + 3); // Play for 0.3 seconds
  }

  const handleInitialize = () => {
    const webexConfig = {
      fedramp: false,
      logger: {
        level: 'info'
      },
      cc: {
        allowMultiLogin: true
      }
    };
    store.init({ webexConfig, access_token: accessToken }).then(() => {
      setIsInitialized(true);
    });
  };

  const onAccepted = (task) => {
    setIncomingTasks((prevTasks) => prevTasks.filter((t) => t.data.interactionId !== task.data.interactionId));
    console.log('onAccepted Invoked');
  };

  const onRejected = (task) => {
    setIncomingTasks((prevTasks) => prevTasks.filter((t) => t.data.interactionId !== task.data.interactionId));
    console.log('onRejected Invoked');
  };

  const onLoginSuccess = () => {
    setIsStationLogInSuccess(true);
  };

  const onCCSignOut = () => {
    setIsInitialized(false);
    setIsStationLogInSuccess(false);
    console.log('onCCSignOut invoked');
  };

  return (
    <ThemeProvider themeclass="mds-theme-stable-lightWebex">
      <IconProvider iconSet="momentum-icons">
        <div className="App mds-typography">
          {isStationLogInSuccess && (
            <div className="user-state-container">
              <UserState />
            </div>
          )}

          <div className="cc-widget-app">
            {!isInitialized ? (
              <div className="initialization-form">
                <h2>Initialize Widgets</h2>
                <input
                  type="text"
                  value={accessToken}
                  onChange={(e) => setAccessToken(e.target.value)}
                  placeholder="Enter access token"
                />
                <button onClick={handleInitialize} disabled={!accessToken}>
                  Sign In
                </button>
              </div>
            ) : (
              <div>
                <StationLogin onCCSignOut={onCCSignOut} onLogin={onLoginSuccess} />

                <>
                  <TaskList />
                  {store.currentTask && (
                    <div style={{ margin: '5rem 2rem' }}>
                      <CallControlCAD />
                    </div>
                  )}
                </>
              </div>
            )}
          </div>

          {/* Incoming Task Container */}
          {incomingTasks.map((task) => (
            <div key={task.data.interactionId} className="incoming-task-container">
              <IncomingTask
                incomingTask={task}
                onAccepted={() => onAccepted(task)}
                onRejected={() => onRejected(task)}
              />
            </div>
          ))}
        </div>
      </IconProvider>
    </ThemeProvider>
  );
}

export default observer(App);
```

2. Add the following code to the `index.jsx` file:

```js
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

const container = document.getElementById('root');

if (!container) throw new Error('Failed to find the root element');

container.style.height = '100%';
const root = createRoot(container);

root.render(<App />);
```

3. Add the following styles to the `App.css` file:

```css
.App {
  height: 100vh;
}

.cc-widget-app {
  padding: 1rem;
  color: var(--mds-color-theme-button-primary-normal);
  background-color: var(--mds-color-theme-inverted-text-primary-normal);
}

.initialization-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  padding: 30px;
  background-color: #f5f5f5;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.initialization-form h2 {
  margin: 0 0 20px 0;
  color: #333;
}

.initialization-form input {
  width: 300px;
  padding: 12px;
  border-radius: 25px;
  border: 1px solid #ddd;
  outline: none;
  font-size: 14px;
  transition: all 0.3s;
}

.initialization-form input:focus {
  border-color: #0052cc;
}

.initialization-form button {
  padding: 12px 24px;
  border-radius: 25px;
  border: none;
  background-color: #0052cc;
  color: white;
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
  transition: background-color 0.3s;
}

.initialization-form button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.user-state-container {
  width: 16rem;
  margin: 1rem 3rem;
}

.incoming-task-container {
  position: absolute;
  bottom: 20px;
  right: 20px;
  z-index: 1000;
}
```

We have added the following widgets from the Webex Contact Center:

- `StationLogin` allows you to select the type of channel you want to use for establishing the voice connection. Options include `Desktop`, which uses WebRTC; `Extension`, which allows using a softphone; and `Dial Number`, which allows using a PSTN number.
- `UserState` shows the agent's availability.
- `TaskList` shows all the tasks an agent is currently handling.
- `CallControlCAD` provides all the controls related to an ongoing call.
- `IncomingTask` shows and handles incoming calls.

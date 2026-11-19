---
type: Guide
title: Webex Contact Center Web Widgets | Quickstart
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/cc-web-widgets-quickstart
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-quickstart)

This Quickstart Guide walks you through integrating Webex Contact Center capabilities using React widgets into your application from the ground up. Follow these steps to create a fully functional application.

## Prerequisites

- **Node.js** (v20 or higher) and **yarn** (or **npm**) installed
- A **Webex Contact Center sandbox account** if you don't have a **Contact Center Org account**. [Create one here](https://developer.webex.com/webex-contact-center/docs/sandbox_cc)
- An **access token** from the [developer portal](https://developer.webex.com/). Click on your profile icon, and you’ll see a screen where you can copy the access token.
- A code editor (VS Code, WebStorm, etc.)

## Create Project Structure

Create a project structure as shown below.

```shell
my-cc-project/
├── public/
│   └── index.html          # HTML entry point
├── src/
│   ├── App.jsx             # Main application component
│   ├── App.css             # Main application css
│   └── index.jsx           # Application entry point
├── package.json            # Project dependencies
└── webpack.config.js       # Webpack configuration
```

## Update the package.json File

```json
{
  "name": "My CC Project",
  "version": "1.0.0",
  "scripts": {
    "start": "webpack serve",
    "build": "webpack --mode production"
  },
  "dependencies": {
    "@momentum-ui/react-collaboration": "26.201.9",
    "@webex/cc-widgets": "1.28.0-next.3",
    "react": "18.3.1",
    "react-dom": "18.3.1"
  },
  "devDependencies": {
    "@babel/core": "7.28.5",
    "@babel/preset-env": "7.28.5",
    "@babel/preset-react": "7.28.5",
    "babel-loader": "10.0.0",
    "css-loader": "7.1.2",
    "html-webpack-plugin": "5.6.5",
    "husky": "9.1.7",
    "sass": "1.94.2",
    "sass-loader": "16.0.6",
    "style-loader": "4.0.0",
    "webpack": "5.103.0",
    "webpack-cli": "6.0.1",
    "webpack-dev-server": "5.2.2"
  }
}
```

**Note**:

1. For bundlers other than webpack, install and configure the dependencies accordingly.
2. Adding `husky` is only required when using npm instead of yarn. Use `npm install --ignore-scripts` if you remove it from the `package.json` file.

Add the following to the `package.json` if you are using `yarn`:

```json
"resolutions": {
  "@momentum-design/components": "0.53.8",
  "@momentum-design/icons": "0.17.0",
  "@momentum-design/brand-visuals": "0.10.0"
}
```

Add the following to the `package.json` if you are using `npm`:

```json
"overrides": {
  "@momentum-design/components": "0.53.8",
  "@momentum-design/icons": "0.17.0",
  "@momentum-design/brand-visuals": "0.10.0"
}
```

## Install Dependencies

Run the following command based on your project configuration:

```shell
yarn install
```

or

```shell
npm install
```

## Webpack Configuration

Add the following configuration to the `webpack.config.js` file. If you are using a different bundler, configure similar settings.

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.jsx',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
    clean: true
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', ['@babel/preset-react', { runtime: 'automatic' }]]
          }
        }
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
      {
        test: /\.s[ac]ss$/i,
        use: ['style-loader', 'css-loader', 'sass-loader']
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource'
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource'
      }
    ]
  },
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx', '.json'],
    fallback: {
      worker_threads: false
    }
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
      filename: 'index.html'
    })
  ],
  devServer: {
    static: {
      directory: path.join(__dirname, 'public')
    },
    client: {
      overlay: {
        errors: true, // You can still show errors
        warnings: false // Disable warnings in the overlay
      }
    },
    compress: true,
    port: 3000,
    hot: true,
    open: true
  },
  devtool: 'source-map'
};
```

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

## Run Application

Start the development server:

```shell
yarn start
```

or

```shell
npm start
```

This will:

- Start webpack-dev-server
- Open your browser automatically at `http://localhost:3000`
- Enable hot module replacement (changes auto-refresh)

## Test Your Application

1. **Open the application** in your browser (http://localhost:3000)
2. **Enter your access token** in the input field. This can be obtained from the [Developer Portal](https://developer.webex.com). You can log in to the Developer Portal using one of the users from your Contact Center Org account or the test users from the sandbox account.
3. **Use StationLogin** to select your connection type (Desktop/Extension/Dial Number)
4. **Change agent state** using the `UserState` widget to `Available`
5. Make a call to the entry point number from a softphone (you can use the [Webex Web Calling Client](https://web.webex.com/calling?calling)). Here you can log in to the softphone using one of the users from your Contact Center Org account or the test users available in the sandbox account.
6. You should be able to receive the call on the Webex Contact Center Widgets application you created above.

**Congratulations!** 🎉 You now have a fully functional Webex Contact Center Widgets application running from scratch.

## Kitchen Sink App

Please visit our [kitchen sink app](https://widgets.webex.com/samples-cc-react-app/index.html) to try out all the available widgets.

## Known Issues/Limitations

- Changing the versions of dependencies other than what is mentioned in the `package.json` file section above might break the application, so please use all the versions as specified in this guide.
- Error after transferring call: When you refresh the page while you have an incoming call, the `onAcceptCallback` on the `IncomingTask` widget is not invoked.

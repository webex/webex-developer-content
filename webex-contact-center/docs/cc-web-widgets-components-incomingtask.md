---
type: Guide
title: Webex Contact Center Web Widgets | Components | IncomingTask
display_title: IncomingTask
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-incomingtask
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-incomingtask)

The `IncomingTask` component presents incoming tasks to agents and provides actions to accept or reject them.

---

The `IncomingTask` component displays incoming contact center tasks (such as calls, chats, emails) and allows agents to take action on them. The component provides a clear interface for agents to:

- View incoming task details
- Accept incoming tasks (For **Desktop** calls only)
- Decline incoming tasks (For **Desktop** calls only)

**Look and feel**:

![incoming-task.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt92631c28fffeeb81/6972a15f446329996b6a3f21/incoming-task.png?branch=integration&width=560)

## Import

```js
import { IncomingTask } from '@webex/cc-widgets';
```

## Props

| Prop           | Type             | Required | Description                                         |
| -------------- | ---------------- | -------- | --------------------------------------------------- |
| `incomingTask` | `object`         | Yes      | The incoming task object containing task details    |
| `onAccepted`   | `(task) => void` | No       | Callback function triggered when a task is accepted |
| `onRejected`   | `(task) => void` | No       | Callback function triggered when a task is rejected |

## Usage Example

### App level State Management

```js
import React, { useState, useEffect } from 'react';
import { store } from '@webex/cc-widgets';

function App() {
  const [incomingTasks, setIncomingTasks] = useState([]);

  useEffect(() => {
    // Set up incoming task callback
    store.setIncomingTaskCb(({ task }) => {
      console.log('Incoming task:', task);
      setIncomingTasks((prevTasks) => [...prevTasks, task]);
      playNotificationSound(); // Check the Quickstart guide for sample code
    });

    return () => {
      store.setIncomingTaskCb(undefined);
    };
  }, []);
}
```

### Widget

```js
<div>
  {
    incomingTasks.map((task) => (
      <div key={task.data.interactionId} className="incoming-task-container">
        <IncomingTask
          incomingTask={task}
          onAccepted={() => onAccepted(task)}
          onRejected={() => onRejected(task)}
        />
      </div>
    ));
  }
</div>
```

Callbacks

```js
const handleAccept = (task) => {
  console.log('Task accepted:', task);
};

const handleReject = (task) => {
  setIncomingTasks((prevTasks) => prevTasks.filter((t) => t.data.interactionId !== task.data.interactionId));
  console.log('Task rejected:', task);
};
```

**Note**:

1. `task` object in the `IncomingTask` can be passed by listening to `store.setIncomingTaskCb(callback);`. Please refer to the [Quickstart Guide's](https://developer.webex.com/docs/cc-web-widgets-quickstart) Webex Contact Center Integration section.
2. State management needs to be done at the application level as shown above.

## Features

- Visual notifications for incoming tasks
- Accept/Reject action buttons for `Desktop` and `Digital` tasks

## Configuration Notes

- The component requires the `store` to be initialized with a valid access token
- Agent must be in `Available` state to receive tasks
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design

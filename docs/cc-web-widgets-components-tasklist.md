---
type: Guide
title: Webex Contact Center Web Widgets | Components | TaskList
display_title: TaskList
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-tasklist
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-tasklist)

The `TaskList` component renders and manages a list of active tasks for the agent.

---

It provides a comprehensive view of all active tasks assigned to the agent. It allows agents to:

- View multiple tasks simultaneously
- Select tasks to focus on
- Accept/Decline pending tasks from the list
- See task details and status

**Look and feel**:

![task-list](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt58315177e3fbe15c/6972a51190363d3dbac2971e/task-list.png?branch=integration&width=560)

## Import

```js
import { TaskList } from '@webex/cc-widgets';
```

## Props

| Prop             | Type             | Required | Description                                                       |
| ---------------- | ---------------- | -------- | ----------------------------------------------------------------- |
| `onTaskAccepted` | `(task) => void` | No       | Callback function triggered when a task is accepted from the list |
| `onTaskDeclined` | `(task) => void` | No       | Callback function triggered when a task is declined from the list |
| `onTaskSelected` | `(task) => void` | No       | Callback function triggered when a task is selected               |

## Usage Example

Widget

```js
<TaskList onTaskAccepted={handleTaskAccepted} onTaskDeclined={handleTaskDeclined} onTaskSelected={handleTaskSelected} />
```

Callback

```js
const handleTaskAccepted = (task) => {
  console.log('Task accepted from list:', task);
};

const handleTaskDeclined = (task) => {
  console.log('Task declined from list:', task);
};

const handleTaskSelected = (task) => {
  console.log('Task selected:', task);
};
```

## Configuration Notes

- The component requires the `store` to be initialized with a valid access token
- Agents must be logged in and in an appropriate state to see tasks
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design

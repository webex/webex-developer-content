---
type: Guide
title: Webex Contact Center Web Widgets | List of Widgets
display_title: Overview
canonical_url: https://developer.webex.com/docs/cc-web-widgets-list-components
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-list-components)

Build Contact Center agent interfaces with **Webex Contact Center widget components** from the `@webex/cc-widgets` package. Browse the available components and their import example.

## Webex Contact Center Widget Components

The following React components are available for building your Contact Center agent interface:

### Core Components

1. **[StationLogin](https://developer.webex.com/docs/cc-web-widgets-components-stationlogin)**
   - Allows agents to perform station login and update their profile.
   - Supports multiple connection types: Desktop (WebRTC), Extension (Softphone), and Dial Number (PSTN)

2. **[UserState](https://developer.webex.com/docs/cc-web-widgets-components-userstate)**
   - Displays and manages agent state
   - Allows agents to switch between states (Available, Meeting, etc.)

### Task Management Components

3. **[IncomingTask](https://developer.webex.com/docs/cc-web-widgets-components-incomingtask)**
   - Presents incoming tasks to agents
   - Provides accept and reject actions

4. **[TaskList](https://developer.webex.com/docs/cc-web-widgets-components-tasklist)**
   - Displays and manages multiple tasks in a list view
   - Supports task selection, acceptance, and decline callbacks

### Call Control Components

5. **[CallControlCAD](https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad)**
   - Advanced call controls with Call Associated Data
   - Includes consult, transfer, and conference capabilities
   - Supports styling via `callControlClassName` and `callControlConsultClassName` properties

6. **[OutdialCall](https://developer.webex.com/docs/cc-web-widgets-components-outdialcall)**
   - Enables agents to make outbound calls
   - Manages outdial call workflows

### Digital Channel Components

7. **[DigitalChannels](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels)**
   - Unified interface for chat, email, and social media interactions
   - Handles JWT authentication, conversation state, and theme sync with your application

### AI Assistant Components

8. **[AIAssistant](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant)**
   - Provides an agent-facing AI Assistant panel
   - Includes Real Time Assist for task-scoped suggested responses and feedback

## Import Example

All components can be imported from the `@webex/cc-widgets` package:

```js
import { 
  StationLogin, 
  UserState, 
  IncomingTask, 
  TaskList, 
  CallControlCAD,
  OutdialCall,
  DigitalChannels,
  AIAssistant
} from '@webex/cc-widgets';
```

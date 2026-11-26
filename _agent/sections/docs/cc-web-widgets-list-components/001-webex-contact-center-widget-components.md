---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-list-components
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Contact Center Widget Components
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-list-components). [Full Markdown](../../../../docs/cc-web-widgets-list-components.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build Contact Center agent interfaces with **Webex Contact Center widget components** from the `@webex/cc-widgets` package. Browse the available components and their import example.

## Selected section

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

---
type: Guide
title: Webex Contact Center Web Widgets | Components | DigitalChannels
display_title: DigitalChannels
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels)

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Overview

The component handles digital customer interactions in Webex Contact Center through
one consistent UI that adapts to the active task's channel type.

### Supported Digital Channels

`DigitalChannels` supports the following media types:

| Channel Type      | Media Type Value   | Description |
| ----------------- | ------------------ | ----------- |
| Chat              | chat               | Real-time text-based customer conversations |
| Social            | social             | Social media interactions (Facebook Messenger, WhatsApp, etc.) |
| Email             | email              | Email-based customer communications |

The widget automatically detects the current task's media type and renders the
appropriate interface.

### Key Features

The widget automatically handles:

- JWT token management and authentication
- Conversation initialization and state management
- Theme synchronization with your application
- Real-time message updates and notifications

## Release scope

Digital channel **conference** and **outdial** flows are not included in this release. Those capabilities are planned for **Phase II**; this documentation will be updated when they become generally available.

## Prerequisites

Before implementing the Digital Channels Widget, ensure you have:

1. **Sandbox setup**

   Complete the [Digital Channels – Complete Setup Guide (Lab 12 -
   Digital Channels)](https://webexcc.github.io/pages/Digital/) so your Webex
   Contact Center environment is configured for digital channels. If you need an
   environment, request a [Webex Contact Center
   sandbox](https://developer.webex.com/webex-contact-center/docs/sandbox_cc).

   Follow these labs from the guide:

   - Lab 12.1
   - Lab 12.5
   - Lab 12.7
   - Lab 12.8
   - Lab 12.9
   - Lab 12.10
   - Lab 12.11
   - Lab 12.19

2. **Completed the [Webex Contact Center Web Widgets Quick Start
   Guide](https://developer.webex.com/docs/cc-web-widgets-quickstart)** including:
   - Widgets initialization
   - Authentication setup (Access Token or OAuth)
   - Station Login configuration

3. **Required dependencies:**
   - `@webex/cc-widgets` package installed
   - `@momentum-ui/web-components` (peer dependency)
   - React 18.3.1 or higher

4. **Agent configuration:**
   - Agent must have a Multimedia profile with Digital Channels enabled (Chat,
     Email, and/or Social)
   - Agent must be logged in via Station Login widget
   - Agent must be in an appropriate state to receive digital channel tasks

## Getting Started

Follow these steps to integrate `DigitalChannels` into your application. Install
`@webex/cc-widgets` as described in the [Quick Start Guide](https://developer.webex.com/docs/cc-web-widgets-quickstart) if you have not already.

### Step 1: Import the Widget

Add the following import statement to your component file:

```javascript
import { DigitalChannels } from '@webex/cc-widgets';
```

### Step 2: Add the Widget to Your Application

Add the widget to your component:

```javascript
<DigitalChannels />
```

### Step 3: Configure the Theme (Optional)

The widget supports two themes: Light (default) and Dark. The theme is
automatically read from the store, so you do not need to pass any props to the
widget.

To set the theme, use the store's `setCurrentTheme` method:

```javascript
import { store } from '@webex/cc-widgets';

// Set light theme (default)
store.setCurrentTheme('LIGHT');

// Set dark theme
store.setCurrentTheme('DARK');
```

The Digital Channels Widget will automatically reflect the theme set in the
store.

### Step 4: Handle Digital Tasks

Once the widget is integrated, it will automatically display the appropriate
interface based on the type of digital task assigned to you (Chat, Email, or
Social).

The following sections provide detailed explanations of the interface for each
channel type.

### Feature Walkthrough (Vidcast)

Watch the [Digital Channels Widget – Feature Walkthrough
(Vidcast)](https://app.vidcast.io/share/5f73c3a6-65f2-4a53-819e-1e56375ee433)
for a visual guide to the widget.

## Using the Email Channel

When you receive an email task, the Digital Channels Widget displays the email
interface. This section explains the email features and action buttons available
to you.

### Viewing Your Email List

When you receive an email task, the widget displays a list of all emails in the
conversation thread. Each email entry shows the sender information, timestamp,
status, and a preview of the content.

![Email list view – displays the email conversation thread assigned to the
agent](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt31755d5179e20fa5/69976a1045700700085f50b8/digital-channels-widget-001-email-list-view.png)

| Element           | Description |
| ----------------- | ----------- |
| Task Header       | Shows "Email Task" with a close (×) button |
| Subject Line      | Displays the email subject with a refresh icon |
| Email Entries     | List of individual emails in the thread |
| Sender            | Email address of the sender |
| Timestamp         | Date and time of the email |
| Status Indicator  | Shows "Received" for incoming or "Sent" for outgoing emails |
| Preview Text      | Brief preview of the email content |
| Expand/Collapse   | Chevron icon (∨) to expand or collapse individual emails |

### Reading an Email and Response Options

When you click on an email entry (or the expand arrow), the email expands to
show the full content along with action buttons for responding.

![Email expanded view – shows complete email details with response
options](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta37d05eb1140e6db/69976a101eaffc0008e46086/digital-channels-widget-002-email-expanded-view.png)

**Email header information:**

- **Subject** – Full email subject line
- **From** – Sender's email address
- **Sent** – Full date and time when the email was sent
- **To** – Recipient email address(es)

**Action buttons (displayed at the bottom of the expanded email):**

| Button     | Description |
| ---------- | ----------- |
| Reply      | Respond directly to the sender only |
| Reply All  | Respond to the sender and all recipients in the thread |
| Forward    | Forward the email to another recipient |

**Quick action icons (top-right corner):** Reply, Reply All, Forward, and
Collapse (∧ arrow) to minimize the email.

### Composing and Sending Email Responses

When you click Reply, Reply All, or Forward, the email composer opens so you
can compose and send a response.

![Email reply composer – rich text editor for composing email
responses](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2420158283e72e6e/69976a10b13d650008b4f6c9/digital-channels-widget-010-email-reply-composer.png)

**Composer header:**

- **Subject Line** – Pre-filled with "Re:" prefix for replies
- **Delete Button** – Discard the draft
- **To field** – Recipient (auto-populated for Reply)
- **+ Cc / + Bcc** – Add carbon copy or blind carbon copy recipients

**Rich text formatting toolbar:** Heading, Bold, Italic, Underline, Strikethrough,
text color, numbered list, bullet list, block quote, insert table, insert link,
alignment, attach file, insert template, insert emoji.

**Original email thread:** Displays below a separator with Subject, From, Sent,
and To from the original email.

**Action buttons:** Clear (clears composer content) and Send (sends the email
response).

## Using the Chat Channel

When you receive a chat task, the Digital Channels Widget displays the chat
interface. This section explains the chat features and how to interact with
customers in real time.

### Viewing the Chat Conversation

When you accept a chat task, the widget displays a real-time conversation
interface with customer information, message history, and a compose area.

![Chat conversation view – real-time messaging interface between agent and
customer](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd0e888b0f18c4a1e/69976a268d3a6a0008c5a8fc/digital-channels-widget-028-chat-conversation-view.png)

**Task header:** Shows "Chat Task" with a close (×) button.

**Customer information card:** Customer name (with verification checkmark) and
email address.

**Message display area:** All messages (agent and customer) appear on the left,
distinguished by styling and labels:

| Message Type       | Display Format |
| ------------------ | -------------- |
| Agent Messages     | "You" as sender label, with timestamp and "Delivered" status |
| Customer Messages  | Customer name with avatar initial, timestamp, and "Received" status |

**Message components:** Avatar, sender label, timestamp, status, and message
content.

### Understanding Auto-Generated Welcome Messages

When a chat session begins, the system may display an auto-generated welcome
message from the customer's side.

![Chat interface with auto-generated welcome message and customer information
card](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltec92a81cd2d39373/69976a26348aa80008ceea52/digital-channels-widget-029-chat-welcome-message.png)

**Auto-generated message:** Shown in a speech bubble from the customer side with
an "Auto Generated" label and welcome text (e.g., "Welcome to Webex CC Chat").

### Composing and Sending Chat Messages

The message compose area at the bottom provides options for composing and
sending messages.

![Chat message input area – tools for composing
messages](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc790e670ca4f8e25/69976a260e0ada0008af97ff/digital-channels-widget-030-chat-input-area.png)

**Input toolbar icons:**

- Attach file
- Insert template (canned responses)
- Text formatting
- Insert emoji
- Trigger Workflow
- Save as Draft

**Message input field:** Placeholder "Write a message to [Customer Name]" with
character counter (e.g., 0 / 2000).

**Send button:** Bottom-right; enabled when the message field contains text,
disabled when empty.

**Clear button:** Bottom-left; appears when the agent has typed a message;
clears the entire message content.

## Using the Social Channel

When you receive a social media task (Facebook Messenger, WhatsApp, etc.),
the Digital Channels Widget displays the social channel interface. The interface
is similar to the Chat interface, optimized for social media interactions.

![Social channel view – social media conversations with platform-specific
indicators and customer profile information](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2fc87d0773bdd014/69976a50da5d88000881e4cf/digital-channels-widget-041-generic-send-icon.png)

## Troubleshooting

### Widget Not Rendering

**Symptom:** The Digital Channels Widget does not appear.

**Possible causes and solutions:**

| Cause                    | Solution |
| ------------------------ | -------- |
| Widgets not initialized  | Ensure `store.init()` has completed successfully; check console for errors |
| Agent not logged in      | Verify agent has completed Station Login |
| No active digital task   | Widget only renders when there is an active chat, social, or email task |

### Theme Not Applying

**Symptom:** Widget appears but theme is incorrect.

**Solutions:**

- Verify the theme is set in the store using `store.setCurrentTheme('LIGHT')` or
  `store.setCurrentTheme('DARK')`
- Ensure Momentum UI components are properly loaded

### Token or Authentication Errors

**Symptom:** Console shows JWT or token-related errors.

**Solutions:**

- Verify access token is valid and not expired
- Ensure token has required scopes for digital channels
- Check network connectivity to Webex services

## Related Documentation

For comprehensive setup and configuration, refer to:

- [Webex Contact Center Widgets \| Introduction](https://developer.webex.com/docs/cc-web-widgets-introduction)
- [Webex Contact Center Web Widgets \| Quick Start Guide](https://developer.webex.com/docs/cc-web-widgets-quickstart)

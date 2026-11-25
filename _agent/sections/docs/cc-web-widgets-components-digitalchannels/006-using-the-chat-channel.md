---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the Chat Channel
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels). [Full Markdown](../../../../docs/cc-web-widgets-components-digitalchannels.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope](002-release-scope.md) [Prerequisites](003-prerequisites.md) [Getting Started](004-getting-started.md)

## Article introduction

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Selected section

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

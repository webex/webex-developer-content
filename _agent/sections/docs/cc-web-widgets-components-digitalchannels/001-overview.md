---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels). [Full Markdown](../../../../docs/cc-web-widgets-components-digitalchannels.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope](002-release-scope.md) [Prerequisites](003-prerequisites.md) [Getting Started](004-getting-started.md)

## Article introduction

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Selected section

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

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels). [Full Markdown](../../../../docs/cc-web-widgets-components-digitalchannels.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope](002-release-scope.md) [Getting Started](004-getting-started.md)

## Article introduction

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Selected section

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

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting Started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels). [Full Markdown](../../../../docs/cc-web-widgets-components-digitalchannels.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope](002-release-scope.md) [Prerequisites](003-prerequisites.md)

## Article introduction

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Selected section

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

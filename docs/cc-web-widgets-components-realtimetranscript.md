---
type: Guide
title: Webex Contact Center Web Widgets | Components | RealTimeTranscript
display_title: RealTimeTranscript
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-realtimetranscript
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-realtimetranscript)

The `RealTimeTranscript` component renders the live voice transcript for the currently selected task.

## Overview

It is designed for telephony experiences where agents need to follow the ongoing conversation as transcript chunks arrive in real time. The widget reads transcript data from the widgets store and updates automatically as the active task changes.

## Import

```js
import { RealTimeTranscript } from '@webex/cc-widgets';
```

## Props

| Prop | Type | Required | Description |
| --- | --- | --- | --- |
| `className` | `string` | No | Adds a custom CSS class to the root container. |
| `liveTranscriptEntries` | `RealTimeTranscriptEntry[]` | No | Optional fallback transcript entries to render when live store-backed transcript data is not available. |

### RealTimeTranscriptEntry

| key | type | description |
| --- | --- | --- |
| `id` | `string` | Unique entry identifier. |
| `speaker` | `string` | Speaker label shown in the transcript UI. |
| `message` | `string` | Transcript text for the entry. |
| `timestamp` | `number` | Timestamp used for sorting transcript entries. |
| `displayTime` | `string` | Optional formatted time label. |
| `event` | `string` | Optional event label rendered above the transcript line. |
| `isCustomer` | `boolean` | Marks the entry as customer speech for avatar styling. |
| `avatarUrl` | `string` | Optional avatar image URL. |
| `initials` | `string` | Optional avatar initials fallback. |

## Usage

```js
<RealTimeTranscript />
```

With custom styling:

```js
<RealTimeTranscript className="agent-transcript-panel" />
```

With fallback transcript entries:

```js
<RealTimeTranscript
  liveTranscriptEntries={[
    {
      id: 'line-1',
      speaker: 'Customer',
      message: 'Hello, I need help with my order.',
      timestamp: Date.now(),
    },
  ]}
/>
```

## How It Works

- The widget reads the currently selected task from the widgets store.
- When live real-time transcription data is available for that task, the widget maps and renders those transcript entries automatically.
- If there is no active transcript stream yet, the widget falls back to the optional `liveTranscriptEntries` prop.

## Configuration Notes

- Use this widget together with task-selection widgets such as `IncomingTask` or `TaskList`, so the store has a current task to bind to.
- Real-time transcription data is available only when the Contact Center configuration enables the underlying transcript feature for the agent.
- This widget is intended for live voice interactions. If no transcript is available, it renders an empty-state message.

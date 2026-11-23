---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-logging-diagnostics
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Metrics Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-logging-diagnostics). [Full Markdown](../../../../docs/desktop-logging-diagnostics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Create widget loggers and collect, download, and clean up Desktop widget logs.

## Selected section

## Webex Metrics Module

**Availability:** The existing SDK documentation identifies this as an internal module. Confirm its availability with your Cisco contact before relying on it in a third-party widget.
The Webex Metrics module is an internal module that is responsible for monitoring and measuring performance, usage, and behavioral data from widgets.

### Methods
#### trackBehavioralEvent
```typescript
Desktop.webexMetricsInternal.trackBehavioralEvent("Call Consult Clicked",  {
          Status: "Success",
          interactionId: "49bcf26b-ec75-4351-89fa-55d54682c20c",
          media_type: "telephony",
          Reason: "AgentConsultEnded"
        });
```

**Parameters**

| Name    | Type           | Description                        | Required |
|---------|----------------|------------------------------------|----------|
| name | string | Name of the event to be tracked | Yes |
| options | EventPayload | Additional data included in the event payload | No |

The `trackBehavioralEvent` function is used to log and track user interactions and behavioral events within widgets. It takes an event name and an optional options object as parameters.

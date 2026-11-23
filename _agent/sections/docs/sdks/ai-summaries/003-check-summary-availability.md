---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Check summary availability
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Check summary availability

Generation requires both the organization-level configuration flag and the corresponding task capability:

| Feature | Contact Center configuration | Task capability |
| --- | --- | --- |
| Mid-call | `generatedSummaries.consultTransferSummariesEnabled === true` | `task.aiSummaryCapabilities.midCallEnabled === true` |
| Post-call | `generatedSummaries.wrapUpSummariesEnabled === true` | `task.aiSummaryCapabilities.postCallEnabled === true` |

The SDK rejects a request if either gate is missing or false. Configure organization flags through Contact Center; use the task capability snapshot and updates to control generation actions in your UI. The summary APIs add no station or destination restrictions beyond those of the underlying call flow and tenant configuration.

Both task capabilities initially default to `false`. Read `task.aiSummaryCapabilities` when binding a task and subscribe to `TASK_EVENTS.TASK_FEATURE_ENABLEMENT` for subsequent changes. Reading the snapshot also handles an update that arrived before listener registration.

Bind the received-summary listener at the same time, independently of generation controls. Attach it before answering an offered call: a late listener or restored session is not guaranteed to receive previously delivered summaries.

```typescript
import {TASK_EVENTS} from '@webex/contact-center';
import type {
  AISummary,
  AISummaryFeatureEnablement,
  ITask,
} from '@webex/contact-center';

export function bindSummaries(
  task: ITask,
  updateAvailability: (midCall: boolean, postCall: boolean) => void,
  showReceivedSummary: (summary: AISummary) => void
): () => void {
  const refresh = (_event?: AISummaryFeatureEnablement): void => {
    const {midCallEnabled, postCallEnabled} = task.aiSummaryCapabilities;
    updateAvailability(midCallEnabled, postCallEnabled);
  };

  task.on(TASK_EVENTS.TASK_FEATURE_ENABLEMENT, refresh);
  task.on(TASK_EVENTS.TASK_MID_CALL_SUMMARY_RECEIVED, showReceivedSummary);
  refresh();

  return () => {
    task.off(TASK_EVENTS.TASK_FEATURE_ENABLEMENT, refresh);
    task.off(TASK_EVENTS.TASK_MID_CALL_SUMMARY_RECEIVED, showReceivedSummary);
  };
}
```

Call the cleanup function when replacing the task or unmounting its view. Associate displayed summaries and pending results with their originating task so an old result cannot update another interaction.

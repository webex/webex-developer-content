---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ai-summaries
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Summary payloads and responses
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ai-summaries). [Full Markdown](../../../../../docs/sdks/ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Beta limitations and error handling](007-beta-limitations-and-error-handling.md)

## Article introduction

Add AI-generated summaries to a Webex Contact Center SDK application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Summary payloads and responses

### Task API reference

| Method | Result |
| --- | --- |
| `requestMidCallSummary(action)` | `Promise<AISummary>` for `'CONSULT'` or `'TRANSFER'`. |
| `sendMidCallSummaryResponse(response, action)` | `Promise<void>` acknowledging the consult or transfer summary report. |
| `requestPostCallSummary()` | `Promise<AISummary>` for post-call review. |
| `sendPostCallSummaryResponse(response)` | `Promise<void>` acknowledging the post-call summary report. |

### Render available content

`AISummary` requires `conversationId`; its content fields are optional. Render the fields present in the payload rather than assuming a fixed sentence or format.

| Field | Handling |
| --- | --- |
| `sections` | Structured text: `reasonForTransferOrConsult`, `initialContactReason`, `additionalContactReasons`, `additionalContext`, `keyActionsTaken`, and `nextSteps`. Preserve the keys when reporting edited sections. |
| `summaryText` | Plain-text fallback when structured text is unavailable. |
| `adaptiveCard` and `editAdaptiveCard` | Optional card content. Render supported formats in your application; a card-only payload can contain usable content. |
| `suggestedWrapUpCodes` and `suggestedWrapUpCodesMessage` | Optional wrap-up suggestions and explanatory text. |

Check other optional fields before use. For example, the type does not require a sender name or a consult/transfer action field.

### Build the response

Every `AISummaryResponse` requires:

| Field | Value |
| --- | --- |
| `summary` | Reviewed structured sections or a string. |
| `feedback` | `'none'`, `'thumbs_up'`, or `'thumbs_down'`. |
| `state` | A response state from the table below. |
| `numberOfTimesViewed` | Actual view count. |
| `numberOfTimesEdited` | Actual edit count. |
| `numberOfTimesCopied` | Actual copy count. |

The SDK reports the supplied values; your application manages response state and usage counts. The table below is an example UI policy for the supported state values, rather than behavior applied automatically by the SDK:

| State | Application policy |
| --- | --- |
| `DEFAULT` | Content is available and included. |
| `EXCLUDED` | The initiating agent opts out of including the summary in the next consult or transfer submission. |
| `IGNORED` | No content is available, including while generation is pending, unless exclusion or failure determines the state. |
| `NOT_RECEIVED` | Generation failed without producing content; takes precedence over exclusion. |
| `MID_CALL_CANCELLED` | The agent cancels the consult or transfer selection. |

An exclusion choice is local until reporting. Keep the content available and preserve the choice across generation or retry. `EXCLUDED` records the choice for that submission; it does not establish a recipient access policy.

`wrapUpCode` is optional for post-call reporting. The optional `summaryReceived` field is not transmitted by these response methods in this SDK version and cannot serve as a delivery acknowledgement. Your application does not need to supply transport timestamps.

This helper creates an initial response from structured or plain text. Replace the draft with agent-reviewed content and update feedback, state, and counts before reporting:

```typescript
import type {AISummary, AISummaryResponse} from '@webex/contact-center';

export function createSummaryResponse(
  summary: AISummary
): AISummaryResponse | undefined {
  const hasSectionText = Object.values(summary.sections ?? {}).some(
    (value) => typeof value === 'string' && value.trim().length > 0
  );
  const content = hasSectionText ? {...summary.sections} : summary.summaryText;
  if (!content || (typeof content === 'string' && content.trim().length === 0)) {
    return undefined;
  }

  return {
    summary: content,
    feedback: 'none',
    state: 'DEFAULT',
    numberOfTimesViewed: 0,
    numberOfTimesEdited: 0,
    numberOfTimesCopied: 0,
  };
}
```

The helper returns `undefined` when it finds no usable structured or plain text, including for card-only payloads. Handle supported card content separately or show an unavailable-content state; do not submit an empty default response.

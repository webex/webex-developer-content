---
type: Guide
title: Webex Contact Center Widgets AI-generated Summaries Beta
display_title: AI Summaries Beta
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries)

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Beta overview

AI Summaries Beta is available in `@webex/cc-widgets@1.28.0-next.66`, which uses Contact Center SDK `3.12.0-next.159` through its store dependency.

| Workflow | Widget experience |
| --- | --- |
| Mid-call consult or transfer | Agents review, edit, and share a summary from the call controls. They can also exclude it from the submission. |
| Received summary | The receiving agent views read-only conversation context in **Cisco AI Assistant**, with copy and feedback controls. |
| Post-call wrap-up | Agents review and edit the completed conversation summary alongside configured wrap-up reasons. |

This guide covers agent-to-agent voice calls. AI Agent transfer summaries and dropped-call summaries are separate features. Widgets manage summary generation, presentation, editing, feedback, and response reporting; host applications using these controls should not issue duplicate SDK summary requests.

## Set up the host application

Before installing the Beta:

- Complete the [Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart) for the supported React setup, styling, peer dependencies, authentication, and station login. Replace its example Widgets version with the pinned version below.
- Have an administrator enable AI Assistant access and the required summary features for the applicable queues. See [Enable AI Assistant features in Control Hub for Webex Contact Center](https://help.webex.com/article/n9lk3t6/Enable-Cisco-AI-Assistant-for-Contact-Center) for licensing, user-profile, and recording prerequisites. Your host application provides the widget layout; Agent Desktop layout instructions apply to Agent Desktop.
- Check the **Supported languages for Summaries** table in [Multi-language Support for AI Assistant Features](https://help.webex.com/article/nlm6pob/Multi-language-Support-for-AI-Assistant-Features). Availability depends on the feature, locale, and tenant configuration.

Install with npm or Yarn:

```bash
npm install @webex/cc-widgets@1.28.0-next.66
# Alternative
yarn add @webex/cc-widgets@1.28.0-next.66
```

### Initialize and mount the widgets

1. Initialize the shared store with `store.init({webexConfig, access_token})` and await completion. If using `store.init({webex})` with an existing Webex instance, wait for that instance's `ready` event before initializing the store.
2. Mount **CallControlCAD** for the call-control and wrap-up experience, and **AIAssistant** for received summaries. Use the same initialized store for both, along with the station-login and task controls your application requires.
3. Complete station login, set the agent to Available, and verify that incoming calls and normal call controls work.

No separate AI-summary initialization flag is required. Received summaries in Cisco AI Assistant are available independently of Real-time Assist enablement.

### Check feature availability

Each summary type requires both its organization configuration and the interaction-specific task capability:

| Summary | Organization flag | Task capability |
| --- | --- | --- |
| Mid-call | `generatedSummaries.consultTransferSummariesEnabled === true` | `midCallEnabled === true` |
| Post-call | `generatedSummaries.wrapUpSummariesEnabled === true` | `postCallEnabled === true` |

The store and SDK use these values to control availability. A missing or false SDK gate disables the corresponding request. Use the station and destination combinations supported by the underlying call flow and tenant configuration.

## Review and share a mid-call summary

Opening **Consult Request** or **Transfer Request** requests a summary of the conversation so far. The workflow is the same for both actions:

1. During an active voice call, open the consult or transfer action and choose an eligible destination. The examples use **Agent** and the agent search field.
2. Review **Summary to share** against the conversation. Use the edit control to correct the content, the copy control to copy it, and the thumbs controls to provide feedback.
3. To omit the summary from this submission, select **Exclude summary**. Widgets preserve the generated content and disable its edit, copy, and feedback controls while exclusion is selected. The destination remains available if it meets the normal call requirements.
4. Select **Consult** or **Transfer** to proceed, or the footer **Cancel** to leave without starting the action.

The cards illustrate fields such as **Transfer/Consult Reason**, **Details**, and **Actions taken**. Labels can vary with the returned content and renderer. Conversation text and identifying information are redacted in all screenshots.

### Consult request

Review the summary before starting the consult with the selected agent.

![Consult Request with Summary to share, copy, edit and feedback controls, Exclude summary, Cancel and Consult; identities and conversation text are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt25f685fd73b446cc/6ae462ceb706bba69c516739/cc-widgets-ai-summaries-consult.png)

### Transfer request and editing

Review and correct the content before transferring. The edit view displays **Editing** and the editable summary fields.

![Transfer Request with Summary to share, summary controls, Exclude summary, Cancel and Transfer; conversation text is redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt646aa6fea1e5d046/6ae462c3084ab9ef7ee35fb7/cc-widgets-ai-summaries-transfer.png)

![Transfer Request in Editing state with editable summary fields, feedback and exclusion controls; conversation text is redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3c556f4abe152ac1/6ae4630d0ac6661fc6d2fdb0/cc-widgets-ai-summaries-edit.png)

The dialog may also list Queue, Dial Number, and Entry Point destinations. Their availability follows the underlying call flow; summary delivery can differ by destination.

Consult and transfer remain subject to their normal task-state and destination checks. Summary reporting is handled independently of the call operation, and an unavailable summary does not prevent an otherwise valid call action. If generation fails, use **Retry** when offered. Closing the dialog does not cancel an already active call operation.

## View a received summary

The receiving agent can view shared content without requesting another summary:

1. Receive the consult or transfer.
2. When **Transfer summary available** appears, select **View summary** to open Cisco AI Assistant, or **Later** to dismiss the notification. If the assistant is already open, review the summary there.
3. Review the received context. Received cards are read-only; use their copy and feedback controls as needed.
4. After choosing **Later**, reopen or restore Cisco AI Assistant during the interaction to view the retained summary.

![Cisco AI Assistant displaying a received mid-call summary with copy and feedback controls; sender identity, timestamp and conversation text are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt985b73a4399746a0/6ae463383ab81bbf97fbe473/cc-widgets-ai-summaries-received.png)

**Later** dismisses the notification without discarding the summary. The panel displays summaries for the current interaction. Widgets keep received cards associated with their originating interaction and handle card-specific feedback. A failed feedback submission preserves the previous selection and does not prevent viewing the summary.

## Review a post-call summary

During wrap-up, **Wrap Up Reasons** displays **Summary of your conversation** beside the configured reason selector:

1. End the call and open **Wrap Up Reasons**.
2. Review the summary, correct editable content, and copy it or provide feedback as needed.
3. Choose a valid configured reason in **Search topic**. If an AI-suggested reason is available, review it and select the matching configured reason, or choose another manually.
4. Select **Submit Wrap Up** to complete wrap-up. Selecting a suggestion alone does not submit it.

![Wrap Up Reasons with Search topic, No suggestion available, Summary of your conversation, summary controls and Submit Wrap Up; conversation text is redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3345620941bbd266/6ae4636fd777730bfcfb39d0/cc-widgets-ai-summaries-wrap-up.png)

A summary can be available without a suggested reason. When **AI-suggested: No suggestion available** appears, or a suggestion has no valid configured match, select a configured reason manually.

Summary generation and reason selection are independent. A valid selected reason can keep **Submit Wrap Up** available while generation is pending. Widgets report the selected code identifier and complete task wrap-up separately, without waiting for summary-reporting acknowledgement.

## Beta behavior and troubleshooting

- **Review generated content.** Check summaries against the conversation before sharing or completing wrap-up. Received summaries are read-only; initiating and post-call summaries support editing.
- **Received-card format.** The received-summary view requires Adaptive Card content in this Beta. Plain-text-only payloads display an unavailable state.
- **Session history.** Received-summary history can remain in memory after task cleanup. It is not persistent browser storage: logout clears it, and a page refresh does not restore it.
- **Failure handling.** A failed generation attempt can leave earlier content visible. Use manual **Retry** when offered. Summary reporting does not block valid consult, transfer, or wrap-up actions; do not assume automatic reporting retries.
- **Diagnostics.** Keep access tokens and conversation content out of logs and reports.

| Symptom | Check or recovery |
| --- | --- |
| No Summary to share | Check the pinned Widgets release, both availability gates, and the eligible task. Verify normal call controls first. |
| No received notification or content | Check the destination, exclusion choice, and completed consult or transfer. Show Cisco AI Assistant for the receiving interaction. |
| Incorrect generated content | Correct an editable summary before submission and provide feedback. |
| No suggested wrap-up reason | Select a configured reason manually; summary content and reason suggestions are independent. |
| Generation or reporting error | Record the visible error and call state without sensitive data. Retry generation if offered and check the call operation separately. |

## Try the Beta and verify your integration

Use the [Contact Center Widgets React sample](https://widgets.webex.com/samples-cc-react-app/index.html) with an authorized test environment, a caller, two eligible agent sessions, and configured wrap-up reasons. Initialize it with the test agent's access token. In **Select Widgets to Show**, enable **AI Assistant**, which is not selected by default, and the station-login, agent-state, incoming-task, and call-control surfaces. Check the sample's deployed version; it can differ from this guide's pinned Beta.

Watch [Agent Handoff and post call summaries](https://app.vidcast.io/share/9b04e255-997b-4e73-94ea-dfe03acdefb3) (1 minute 55 seconds), by Ravi Chandra Sekhar Sarika, for a demonstration of mid-call review, receiving-agent context, and post-call wrap-up.

Run the following checks in your host application. Record the build, configuration, and observed results, then complete the test calls and session cleanup.

| Area | Verify |
| --- | --- |
| Setup and availability | Initialize the shared store, log in, accept a call, and confirm each summary flow follows its organization and task gates. |
| Consult and transfer | Review and edit content, complete each call action, and verify received content separately. Exercise exclusion and cancellation. |
| Received summaries | Open content with **View summary**, defer with **Later**, then reopen it. Check read-only display, copy, and card-specific feedback. |
| Post-call wrap-up | Edit the summary and submit a valid reason. Confirm suggestions require agent selection and manual reasons remain usable without suggestions. |
| Failures and session lifecycle | Exercise missing content, generation failure, and **Retry**. Check that new interactions do not show unrelated summaries and logout clears summary state. |

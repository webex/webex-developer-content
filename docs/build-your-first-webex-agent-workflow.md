---
type: Guide
title: Build Your First Webex Agent Workflow
display_title: Build Your First Webex Agent Workflow
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
content_type: documentation
product_group:
- webex-suite
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/build-your-first-webex-agent-workflow)

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## What you will build

You will guide an agent through a small collaboration task: turn three supplied status facts into an update for a Webex test space. The agent uses Webex tools to check the destination and verify the result. You review the destination and message before allowing the write.

The workflow is **inspect → draft → approve → post → verify**. This tutorial uses synthetic facts and an existing test space; it does not require an application deployment or a custom MCP server.

## Before you start

You need:

- VS Code with GitHub Copilot and a session that can use MCP tools. Organization policy must permit the connection.
- A Webex account that can access and post in a dedicated test space. Use a space whose members have agreed to receive tutorial messages.
- Administrator enablement of the [Messaging MCP Server](https://developer.webex.com/docs/messaging-mcp-server), access for your user, and the three tools listed below. Follow [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub) if administrator setup is needed.

Use only synthetic content. Keep credentials out of prompts, screenshots, source files, and chat transcripts.

### Tools and scopes

This workflow uses these capabilities from the Messaging MCP Server:

| Tool | Purpose | Tool scope |
| --- | --- | --- |
| `webex-get-space` | Inspect the destination space. | `spark:rooms_read` |
| `webex-create-message` | Post the approved plain-text update. | `spark:messages_write` |
| `webex-get-message` | Retrieve the posted message for verification. | `spark:messages_read` |

`spark:mcp` is also required for the server connection. A Webex Client Identity Token (WCIT) starts with that connection scope; supported clients use MCP elicitation to request additional tool scopes at runtime. Follow the [Webex MCP authentication guide](https://developer.webex.com/docs/webex-agentic-mcp-servers#authentication) for the authentication method your client supports.

Scope consent, administrator enablement, and your account's access to a space are separate requirements. A connection alone does not establish permission to post.

## Connect the client and set approvals

1. Open the [Messaging MCP Server guide](https://developer.webex.com/docs/messaging-mcp-server) and copy its server URL.
2. Follow the token-based setup in [Connect VS Code to a Webex MCP server](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode), using the Messaging server URL. Generate and enter the token through the documented setup flow, rather than asking the agent to handle it.
3. Start the server and confirm that its tools are available in your Copilot session. Inspect the current tool descriptions and input schemas before using them; the prompts below express the task rather than hard-coding a tool-call payload.
4. Initially expose only `webex-get-space` and `webex-get-message` from this server to the session. Keep unrelated tools unavailable for this exercise.
5. Use manual tool approvals. Before enabling `webex-create-message`, configure it to require confirmation and remove any saved pre-approval for that tool. Follow [VS Code's tool approval guidance](https://code.visualstudio.com/docs/agents/run/approvals#tool-approval). Do not use a mode that approves every call automatically.

The instruction to wait for approval is part of this workflow. Keep the client's write-approval control enabled as well.

## Inspect the destination

In the prompts, replace `YOUR_TEST_SPACE_TITLE` with the exact name of your test space. After the first lookup, replace `YOUR_TEST_ROOM_ID` with the returned identifier. These are input placeholders, not values to send unchanged.

```text
Use only the Webex Messaging MCP Server's read tools.
Find the group space with the exact title YOUR_TEST_SPACE_TITLE.
Show its title and room ID from the tool result.
If there are no matches or more than one match, stop and ask me to identify
the intended space. If the available results are incomplete, ask me for the
exact room ID instead of assuming a unique match.
Do not create, change, or delete anything.
```

Inspect the tool call and its returned data. Confirm the destination against the test space in the Webex app, then keep its room ID for the remaining steps. Matching titles alone are insufficient when several spaces share a name. If the agent cannot resolve one destination, do not continue to a write.

## Draft the update without posting

Use the supplied facts below. No production conversation or customer data is needed.

```text
Prepare a short plain-text update for test space YOUR_TEST_ROOM_ID.
Use only these synthetic facts:
- The demo integration connected successfully.
- The read-only space lookup passed.
- The next step is to test one approved message.

Prefix the draft with a unique marker I can search for:
AGENT-LAB-YOUR_UNIQUE_RUN_LABEL

Show the complete message and destination room ID. Do not post it.
Do not add recipients, mentions, attachments, or facts I did not provide.
Wait for my explicit approval of the final text and destination.
```

Replace `YOUR_UNIQUE_RUN_LABEL` with a label unique to this attempt. Review the draft for all three facts, the intended room ID, and the absence of invented details.

To test withholding approval, reply:

```text
Do not post this draft. Cancel this attempt and make no changes in Webex.
```

Check the tool history and the test space. This attempt should contain no message-creation call or new message with its marker. If you find a write, stop the exercise and review the client's available tools and approval settings.

## Approve and post one message

For the posting attempt, request a fresh draft with a new marker. Enable `webex-create-message` for this session while retaining its manual approval requirement. Keep the two read tools available.

After reviewing the new draft, give the agent this instruction:

```text
Post exactly the draft I just approved to room ID YOUR_TEST_ROOM_ID.
Use webex-create-message from the Webex Messaging MCP Server once.
Do not change the text, use another destination, add mentions or attachments,
or retry automatically if the result is uncertain.
After a successful creation, use webex-get-message to retrieve that message
by the identifier returned by the creation tool.
Report the message ID, room ID, text, and creation time from the returned data.
If creation or verification fails, report the observed result without claiming
that the message was posted or verified.
```

Before approving the client's write-tool confirmation, inspect its destination and complete text. Reject the call if either differs from the approved draft. If the client offers no confirmation, stop and correct the tool's approval configuration before attempting a write.

You can also reject the write confirmation to exercise the approval boundary. Confirm that the rejected attempt produces no new message before starting another attempt with a new marker.

## Verify the result

A statement from the agent that it posted a message is not sufficient. Check all of the following:

- The tool history shows one successful message creation for the approved destination and text.
- A subsequent message lookup returns the same message ID, destination, and text, including your unique marker.
- The message is visible in the intended test space in the Webex app.

Webex uses `roomId` to identify the destination and `id` to identify a message in its REST API. See [Create a Message](https://developer.webex.com/docs/api/v1/messages/create-a-message) and [Get Message Details](https://developer.webex.com/docs/api/v1/messages/get-message-details) for the underlying API contracts. Inspect your MCP tool's actual result format rather than assuming it is identical to the REST response.

If the write times out or its result is unclear, inspect the test space and available read results before considering another attempt. Do not repeat a create operation merely because the agent did not receive a success response. If a duplicate exists, record the failed check and review what was retried.

## Troubleshoot the workflow

| What you observe | What to check |
| --- | --- |
| Server or tools are unavailable | Check the client connection, organization enablement, and allowed tools. Use the [connection troubleshooting guide](https://developer.webex.com/docs/webex-agentic-mcp-servers#troubleshooting). |
| A tool requests additional consent | Review the requested scope against the operation above. Grant only access appropriate to the test. |
| Access is denied | Check the account, space access, granted scopes, and administrator policy. Do not switch identities or destinations to bypass the denial. |
| Several spaces match | Resolve the intended room ID before drafting or posting. |
| The write has an uncertain result | Check for the unique marker before any new creation attempt. |
| Creation succeeds but read-back fails | Keep the returned identifier and inspect the space. Report verification as incomplete; do not create another message as a verification step. |

## Finish the exercise

Disable the message-creation tool when you no longer need it. If you want to remove the test message, inspect the exact message in the Webex app and delete it manually; do not ask the agent to delete a space or unrelated content. If the connection was temporary, remove it using your client's supported controls and follow the [WCIT revocation guidance](https://developer.webex.com/docs/webex-agentic-mcp-servers#revoking-your-wcit-token) when the token is no longer needed.

Keep a record of the destination check, cancelled attempt, approved creation, and independent read-back. These checks give you a repeatable starting point for a more useful workflow. Continue with the [Agent Skills overview](https://developer.webex.com/docs/agent-skills-overview) to learn how reusable instructions can guide recurring tasks.

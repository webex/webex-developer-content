---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Discovery APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Discovery APIs

These APIs are used to discover the content of an organization.

### Member Enumeration

There are three types of calling members. Each member type has its own enumeration API:

| Member Type | API | Notes |
|-------------|-----|-------|
| People | [List People](https://developer.webex.com/docs/api/v1/people/list-people) | Set `callingData=true` to include calling-specific information. Filter non-calling users by inspecting the `licenses` array. |
| Workspaces | [List Workspaces](https://developer.webex.com/docs/api/v1/workspaces/list-workspaces) | Returns all workspaces in the organization |
| Virtual Lines | [Read the List of Virtual Lines](https://developer.webex.com/docs/api/v1/virtual-line-call-settings/read-the-list-of-virtual-lines) | Returns all virtual lines in the organization |

### Call Queue Enumeration

#### Customer Assist and Call Queues

Use the [Read the List of Call Queue or Customer Assist Queues](https://developer.webex.com/docs/api/v1/features-call-queue/read-the-list-of-call-queue-or-customer-assist-queues) API:

| Queue Type | Parameter |
|------------|-----------|
| Customer Assist Queues | `hasCxEssentials=true` |
| Call Queues | `hasCxEssentials=false` |

#### Queue-Agent Assignments

To retrieve the queue assignments of a given agent, use the [Get Details for an Agent for Call Queue or Customer Assist](https://developer.webex.com/docs/api/v1/features-call-queue/get-details-for-an-agent-for-call-queue-or-customer-assist) API with the same `hasCxEssentials` parameter.

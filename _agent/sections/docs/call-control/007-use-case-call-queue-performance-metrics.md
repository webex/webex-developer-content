---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Use Case: Call Queue Performance Metrics'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Use Case: Call Queue Performance Metrics

This example walks through building an application to extract an organization's call queue performance metrics.

### Step 1: Identify Required APIs

- List call queues in the organization
- Register for `telephony_queueMonitoring` webhooks

### Step 2: Create a Service App

Identify the required scopes:

- `spark-admin:telephony_config_read` — to read call queues
- `spark-admin:calls_read` — to register `telephony_queueMonitoring` webhooks

Create the Service App with these scopes. You can start using it in your own organization without publishing to the App Hub.

### Step 3: Authorize the Service App

1. As an organization administrator, authorize the Service App in Control Hub
2. Retrieve the access and refresh tokens for the authorizing organization

### Step 4: Enumerate Organization Content

Use the [Read the List of Call Queue or Customer Assist Queues](https://developer.webex.com/docs/api/v1/features-call-queue/read-the-list-of-call-queue-or-customer-assist-queues) API to list all call queues.

### Step 5: Set Up WebHooks

1. **Register webhook callback:** Use the Webhooks API to register an org-level webhook for `telephony_queueMonitoring`
2. **Register interest:** Use the interest registration API to register interest for `telephony_queueMonitoring`
3. **Set up refresh:** Create a periodic task to refresh interest registrations before they expire

### Step 6: Receive WebHooks

On webhook reception, extract:

- `actorId` — corresponds to the call queue ID
- Performance metrics from `monitoringStatus`: `averageHandlingTime`, `expectedWaitTime`, `averageSpeedOfAnswer`, `longestWaitTime`, `numCallsInQueue`, `numAgentsAssigned`, `numAgentsStaffed`, `numStaffedAgentsIdle`, `numStaffedAgentsUnavailable`

### Step 7: Correlate Data

Match the queue ID from the webhook with queue details from enumeration to display queue names alongside performance metrics.

### Step 8: Publish the Service App

When ready, submit the Service App for publication on the Webex App Hub. Once published, any organization administrator can authorize it.

<a id="webhook-payload-schemas"></a>

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Verify the integration

Test the complete path with the customer after the feature and flow are
published:

1. Confirm that the datasource is active and belongs to the intended
   organization.
1. Confirm that the selected Service App and datasource ID match your
   onboarding record.
1. For a gRPC gateway, confirm that `ListVirtualAgents` returns the expected
   customer-eligible catalog and that Flow Designer can discover and invoke the
   selected virtual agent.
1. Confirm that Webex reaches the gateway and that the gateway validates the
   signed request for the expected organization.
1. Test a caller's conversation, error handling, and any transfer or fallback
   path.

A direct gateway health check or `grpcurl` test is not sufficient. The
meaningful test is the full path from Flow Designer through Contact Center
configuration and datasource resolution to your gateway.
Use the [BYOVA overview](https://developer.webex.com/docs/bring-your-own-virtual-agent) and the selected
protocol guide to validate the feature, flow, and gateway configuration
together.

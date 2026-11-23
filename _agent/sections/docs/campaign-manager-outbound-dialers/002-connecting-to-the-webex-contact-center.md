---
type: Excerpt
canonical_url: https://developer.webex.com/docs/campaign-manager-outbound-dialers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Connecting to the Webex Contact Center
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/campaign-manager-outbound-dialers). [Full Markdown](../../../../docs/campaign-manager-outbound-dialers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Campaign Manager Requirements](001-campaign-manager-requirements.md)

## Article introduction

A Campaign Manager (CM) is designed with the functionality and features to increase right party contacts and meet campaign objectives in an outbound environment by intelligently managing customer contacts as they move through the system. LCM enables contact centers to reach the right people at the right number to best meet campaign objectives.

---

An outbound campaign dialer is a tool used in call centers and telemarketing to automate the process of making outgoing calls to a list of contacts. The dialer helps increase efficiency, improve agent productivity, and optimize campaign performance. The Webex Contact Center Dialer using the Next Generation Media Platform (RTMS) supports the following types of pacing modes:

- **Progressive**
  - The dialer automatically dials a pre-defined number of contacts, one after another once an agent is available.
  - Calls are connected to agents in a sequential manner, ensuring that agents are available to handle each call.
- **Predictive**
  - Uses predictive algorithms to anticipate how many calls to dial when an agent becomes available.
  - Calls are dialed in anticipation of agent availability, aiming to minimize idle time and maximize the number of answered calls.
  - The dialer adjusts the dialing rate based on historical call data and agent performance.
- **IVR**
  - Can be run in either progressive or predictive mode.
  - Calls are dialed based on the configured dialing rate and on IVR port availability.
  - If run in predictive mode, the dialing rate is adjusted based on historical call data to maintain configured abandoned rate.
- **Preview**
  - The dialer presents a preview of the contact, with opted customer information, to the agent before dialing.
  - If the agent accepts the contact, the call is dialed and connected to the agent.
  - If the agent skips or removes the contact, an appropriate call disposition is sent to the Campaign Manager and a new contact is presented to the agent.
  - Can be run in either standard or direct preview mode.
    - In standard mode, CPA(Call Progress Analysis) can be performed to determine if the call was answered by a live customer or an answering machine.<br>
      Based on the CPA result, the dialer can connect the call to agent or send appropriate call disposition to the Campaign Manager.
    - In direct mode, CPA is not performed and the dialer directly connects the call to the agent.
  - The dialing rate can only be 1.0 in both preview modes.

## Selected section

## Connecting to the Webex Contact Center

A custom connector is required to enable the Webex Contact Center to authenticate with your Call Manager resource domain.  This connector is utilized by the Dialer only to obtain the token for subsequent requests to the Campaign Manager. To configure the connector:

1. Login into Webex Admin Portal (Control Hub): [https://admin.webex.com](https://admin.webex.com).
2. Choose **Contact Center** in the left-hand navigation.
3. Scroll down to **Integrations** under **TENANT SETTINGS**.
4. In the **Integrations** page choose **Custom Connectors** to register your campaign manager’s URL.
5. Enter the information requested in **Set Up Custom Connector**.  The custom connector name must be **CampaignManagerCredential**

**Note:** Once your Campaign Manager endpoint is authenticated, the fetch list URI and the call disposition URI can be relative paths that use the same authentication tokens.

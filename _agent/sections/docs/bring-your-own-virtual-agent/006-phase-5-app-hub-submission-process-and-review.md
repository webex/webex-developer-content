---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Phase 5 - App Hub Submission Process and Review
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent). [Full Markdown](../../../../docs/bring-your-own-virtual-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Phase 2 - Authentication](003-phase-2-authentication.md)

## Article introduction

As part of the "Bring Your Own" (BYO) initiative, Webex Contact Center aims to enable seamless integrations with third-party AI providers, enhancing the Webex customer experience with cutting-edge AI innovations. Bring your own Virtual Agent is the first slice of all other other AI functionalities you can bring to Webex Contact Center product offerings.

## Selected section

## Phase 5 - App Hub Submission Process and Review 

All marketplace vendors need to go through the [App Hub Submission Process](https://developer.webex.com/create/docs/app-hub-submission-process). Once you have submitted the app for review, the application will be reviewed against these test cases: 


| Theme | Description |  Priority  |
| ----- | ----------- | ------------ |
| Service App | Service app must be created with a mailer email ID that can be accessed by multiple users in the organization | Optional |
|  | Must provide onboarding documentation for customers | Mandatory |
|  | Support emails, links and documentation must be provided. SLAs for all issues must be mentioned. | Mandatory |
| Bring your own Data Source | Data Exchange Domains registered must be owned by the service app owner. Testing the application on a 3rd party hosting service is permitted but must switch over to a domain that's owned by the service app owner. | Mandatory |
|  | Demostrate logic to generate unique nonce for every customer onboarding the app. | Mandatory |
|  | The logic to decrypt the JWS token received from: [US Public Key](https://idbroker.webex.com/idb/oauth2/v2/keys/verificationjwk/?_gl=1*1vkcvt*_gcl_au*MTcxMTQ5OTI3Ny4xNzM5NTQ0NDUw) or [EU Public Key](https://idbroker-eu.webex.com/idb/oauth2/v2/keys/verificationjwk?_gl=1*1vkcvt*_gcl_au*MTcxMTQ5OTI3Ny4xNzM5NTQ0NDUw) | Mandatory |
|  | Update the nonce for the JWT token at least once every 1440 minutes (24 hours) | Mandatory |
| Customer Setup  | The customer would have to buy 3P-Virtual-Agent SKU to enable your service app | Mandatory |
|  | Customer must be able to discover and authorize your Service App | Mandatory |
|  | Once the app is authorized, the data source must be registered automatically | Mandatory |
|  | Create a "Feature" by navigating to "Contact Center -> Integrations -> Features" and creating a CCAI Config pointing to the Service App created by you. | Mandatory |
|  | The CCAI Config should contain all the required fields necessary for the customer to connect to the project on the AI Vendor's portal | Optional |
| Routing Logic | The customer must be able to configure the "Virtual Agent V2" activity in the flow designer or "VVA Element" in call studio, which points to the CCAI Config created. | Mandatory |
| Health Check | The server must send back the serving status as “SERVING” or “NOT_SERVING” while Cisco initiates Ping Tests. Look here for [sample implementation](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/blob/main/media-service-api/dialog-connector-simulator/src/main/proto/com/cisco/wcc/ccai/v1/health.proto)| Mandatory |
| Call Events | The call must receive and respond to “CALL_START” event when the call is initiated from the entry point | Mandatory |
|  | The Virtual Agent must be able to respond to the caller with a permissable latency of 200 to 500 ms | Mandatory |
|  | The call must end with "CALL_END" event. Showcased via the "debug" tab in the flow designer  | Mandatory |
|  | The call must be escalated to a queue of human agents with "AGENT_TRANSFER" event | Mandatory |
|  | The caller must be able to interupt the Virtual Agent with "BARGE_IN" event | Optional |
|  | The Virtual Agent must be able to process DTMF tones | Optional |
|  | Send custom events, such as vendor config data or call associated data from the flow designer/call studio | Optional |
| Post Call Events | The Virtual agent call must initiate and terminate at the flow designer in the "Virtual Agent V2" activity | Mandatory |
|  | Pass along the Virtual Agent transcript to the agent desktop using custom widget for Webex Contact Center | Mandatory |
|  | Pass along the Virtual Agent transcript to the finesse using custom gadget for UCCE, PCCE and CCE | Mandatory |
|  | Pass along any other insights to the agent desktop such as Virtual Agent Summary, Status or Sentiment Score | Optional |

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Run a reference connector
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Run a reference connector

Clone the [provider sample code](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code), then choose either implementation.

For Java 21 or later:

```bash
cd bring-your-own/virtual-agent/grpc-interface/simulators/byova-grpc-java
./mvnw spring-boot:run
```

For Python 3.10 or later:

```bash
cd bring-your-own/virtual-agent/grpc-interface/simulators/byova-grpc-python
chmod +x run.sh
./run.sh
```

Both samples listen on port `8086` by default. They use local prompts and simple event handling for smoke testing; replace that behavior with your production virtual-agent integration.

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-overview
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Skills Architecture Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-overview). [Full Markdown](../../../../docs/webex-assistant-skills-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex Assistant skills are applications that integrate and complement the Webex Assistant for Devices.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Skills Architecture Overview

We'll begin with a high-level overview of how the Webex Assistant skills platform works within the **Webex Assistant** architecture. The following image is an overview of the architecture:

![Webex Assistant Skills architecture](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbdf7f475647eb961/618bf0affd0d2917d8cfbaf6/skills_architecture-1.png)

We'll start defining the different pieces of the system:

- **Actor**: A user invoking a Skill using the **Webex Assistant**. 
- **Webex Client**: A supported client that can run the **Webex Assistant**. In this case, it is a Webex Device.
- **Assistant Dialogue**: This is what gets the request and decides how to handle it.
- **Assistant NLP**: This is the part of the system that performs machine learning (ML) to analyze the **Actor's** query. Note that this is not used for skills. 
- **Assistant Skills**: This is a cloud service that manages skills created by third party developers like yourself.
- **Third-Party Skill**: This is a cloud service developed by a third-party. It's a service of its own, but it's registered with the **Assistant skills** service in order to be used by the **Webex Assistant**.

The flow works as follows:

1. The **Actor** wakes up Webex Assistant and requests the use of a skill. For example, the **Actor** can say: **OK Webex, tell Echo hello**.
2. The **Webex Client** then forwards that request to the **Assistant Dialogue** service. 
3. The **Assistant Dialogue** services analyzes the query and determines the **Actor** is trying to call a third-party skill. Continuing the example, the **Actor** invoked **Echo** with the query **hello**.
4. The **Assistant Dialogue** checks with the **Assistant skills** service to verify if this particular user has access to the **Echo** skill.
5. If the **Actor** has access to the given Skill, the request goes to the **Assistant skills** service for further processing. 
6. If the requested skill is not available for the **Actor**, then the request goes to **Assistant NLP** for handling instead.
7. The **Assistant skills** service encrypts and signs the request and sends it to the **Third-Party skill** service hosted by a third-party developer.
8. The **Third Party skill** service handles the request and produces a final response, which is then passed back via the same pipeline in reverse to the client.

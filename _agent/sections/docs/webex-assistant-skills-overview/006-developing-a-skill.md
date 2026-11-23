---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-overview
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Developing a Skill
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

## Developing a Skill

Developers can build and implement skills in any preferred programming language and web framework, as long as the proper security components are met, and requests from the **Assistant skills** service match the expected format.

The **Assistant skills** service communicates with **Third-Party skills** via secure HTTPS requests. Skills specify `directives` in order to make control the device response. The response payload also requires a `challenge`. View the Skills Reference guide for more information on [Assistant Directives](https://developer.webex.com/docs/webex-assistant-skills-reference-guide#assistant-directives), and the [Response Payload](https://developer.webex.com/docs/webex-assistant-skills-reference-guide#response-payload) structure.

In the [Assistant Skills SDK Guide](https://developer.webex.com/docs/webex-assistant-skills-guide), we will walk through developing an
Assistant skill using the Webex supported Python SDK, as well as showcase some of the tooling provided. It's important to note that the SDK does not need to be used, but it does have some support for starting and testing a skill.

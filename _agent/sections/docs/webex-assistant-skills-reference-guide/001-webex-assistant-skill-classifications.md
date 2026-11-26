---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-reference-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Assistant Skill Classifications
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-reference-guide). [Full Markdown](../../../../docs/webex-assistant-skills-reference-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

We will go over the structure of the requests sent to your Skill from the **Assistant Skills** service and the
responses expected to be returned from your Skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Webex Assistant Skill Classifications

On the Webex **Assistant skills** service, there are two categories and corresponding status' for skills. The classification of a skill depends on the type of permissions and availability that it has been configured to have by the  developer and the associated organization's administrators.

* Private skill - a skill that has been created on the Assistant skills [Developer Portal](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide)
    * Disabled - Only the developer can invoke the skill. This is the default state of all private skills. 
    * Enabled - Available to all supported Webex Devices for the developer's organization.

* Public skill - a Cisco-approved skill that is available to all Webex organizations through Control Hub.
    * Disabled - No one in the organization has access to the skill 
    * Enabled - Available to all supported Webex Devices for the organization.

By default, whenever a skill is added through the Developer Portal, it will be classified as private with a disabled status. This allows the developer to test and improve the skill on personal-mode devices and on the [Webex Assistant Web Client](https://developer.webex.com/docs/webex-assistant-skills-guide#skill-testing).

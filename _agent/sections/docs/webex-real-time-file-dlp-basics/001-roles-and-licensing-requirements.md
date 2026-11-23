---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-real-time-file-dlp-basics
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Roles and Licensing Requirements
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-real-time-file-dlp-basics). [Full Markdown](../../../../docs/webex-real-time-file-dlp-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex provides a rich set of admin and compliance APIs to help Compliance Officers monitor and assert adherence to corporate policies, as they relate to information exchange and sharing. In this article we introduce the proactive, real-time, file Data Loss Prevention (DLP) compliance mechanism as the preferred way to control proliferation of files in a protected org.

## Selected section

## Roles and Licensing Requirements

The officer responsible for adherence to the corporate policies is called a Compliance Officer, which is a designated role in Control Hub. Notably this role is separate and distinct from that of an admin. The admin role is primarily concerned with the management of the system (user management, device management etc.), while the Compliance Officer role is primarily concerned with the management of content. All compliance APIs check for Compliance Officer scopes before allowing an API request.

In this article we will use the terms Compliance Officer and DLP/CASB (Cloud Access Security Broker) system somewhat synonymously. The CASB/DLP system is a software security framework with preprogrammed and configurable policies which ensures an enterprise adheres to corporate and legal policies. The DLP system uses the Compliance Officer role to interact with the Webex APIs ensuring that these rules and policies are enforced.



> **Info**
>
> The Control Hub GUI allows you to enable real-time file DLP, but you need to either integrate to it according to this article or use a DLP provider that already supports it. If you just turn it on without a functional framework, all file uploads from protected users will incur an additional latency as the default timer expires.





> **Warning**
>
> Org level messages webhooks trigger **only** when real-time file scanning (DLP) is enabled and **only** for messages that contain files.



![Webex Control Hub](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6a4f9d08ae950083/61683e6d5547844ca4abf9b4/control-hub.png)

For a list of Webex compliance and archival partners see [here](https://help.webex.com/en-US/article/nmbm0jk/Webex-Integration-with-Archiving-and-Data-Loss-Prevention-Solutions).

### Licensing

Real-time file DLP needs an enterprise Webex account with the [ProPack license](https://help.webex.com/en-US/article/np3c1rm/Pro-Pack-For-Cisco-Webex-Control-Hub) purchased and applied.

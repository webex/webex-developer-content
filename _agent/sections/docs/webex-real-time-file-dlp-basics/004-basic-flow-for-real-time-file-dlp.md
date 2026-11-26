---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-real-time-file-dlp-basics
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Basic Flow for Real-time File DLP
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-real-time-file-dlp-basics). [Full Markdown](../../../../docs/webex-real-time-file-dlp-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Roles and Licensing Requirements](001-roles-and-licensing-requirements.md)

## Article introduction

Webex provides a rich set of admin and compliance APIs to help Compliance Officers monitor and assert adherence to corporate policies, as they relate to information exchange and sharing. In this article we introduce the proactive, real-time, file Data Loss Prevention (DLP) compliance mechanism as the preferred way to control proliferation of files in a protected org.

## Selected section

## Basic Flow for Real-time File DLP

The real-time file DLP mechanism diverts the flow at which the DLP system is invoked, compared to the current mechanism of event polling. That is, first the DLP system must approve the file, then it will be accessible to other participants. To achieve this flow, without impacting users with too much latency, we are introducing org-wide webhooks for Compliance Officers. An org wide webhook will be sent to the DLP system whenever a protected org user uploads a file. When the DLP system receives the webhook it will extract the content URL of the file in question which it will download via the Compliance Officer role. After inspection, the Compliance system will call either an `approve` on the file content, which will make it accessible to other space members, or a `reject`, which will mark the file as a violation in the space.
While the DLP system scans the file, the users in the space will see a busy indicator until a decision has been made. A default timeout of 10s approves the file in case the DLP system does not respond in time.



> **Info**
>
> Note: The real-time file DLP’s emphasis is on users of a protected organization to not upload and share `sensitive` information to a space. This is different from the also available [Malware protection](https://help.webex.com/en-US/article/yr6g4bb/Anti-Malware-Scanning-of-Files-in-Webex), in which protected users are protected from downloading corrupted files.

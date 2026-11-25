---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-real-time-file-dlp-basics
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Advantages of Real-time File DLP
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-real-time-file-dlp-basics). [Full Markdown](../../../../docs/webex-real-time-file-dlp-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Roles and Licensing Requirements](001-roles-and-licensing-requirements.md)

## Article introduction

Webex provides a rich set of admin and compliance APIs to help Compliance Officers monitor and assert adherence to corporate policies, as they relate to information exchange and sharing. In this article we introduce the proactive, real-time, file Data Loss Prevention (DLP) compliance mechanism as the preferred way to control proliferation of files in a protected org.

## Selected section

## Advantages of Real-time File DLP

The real-time file DLP framework eliminates the polling of the events API for file events (other events like membership and message events still need to be queried from the events API). By its very nature this polling introduces latencies between when a file is accessible in a space until it will be remediated when policy violations mandate such actions. While often only on the order of 1 min, enterprises deemed this latency as too long, as it gave space members an opportunity to inspect, if not download a file.

The advantage of the real-time file DLP API is that a file can be accessed by other space members only after the file has been inspected and approved by the DLP system.

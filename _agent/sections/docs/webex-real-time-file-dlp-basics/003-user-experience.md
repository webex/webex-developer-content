---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-real-time-file-dlp-basics
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- User Experience
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-real-time-file-dlp-basics). [Full Markdown](../../../../docs/webex-real-time-file-dlp-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Roles and Licensing Requirements](001-roles-and-licensing-requirements.md)

## Article introduction

Webex provides a rich set of admin and compliance APIs to help Compliance Officers monitor and assert adherence to corporate policies, as they relate to information exchange and sharing. In this article we introduce the proactive, real-time, file Data Loss Prevention (DLP) compliance mechanism as the preferred way to control proliferation of files in a protected org.

## Selected section

## User Experience

As it relates to the basic user experience of real-time file DLP there are 3 distinct outcomes. A DLP approved file, a default approved file, and a rejected file. Keep in mind that different clients may look slightly different and combining malware scanning with real-time file DLP may also result in slightly different messages.

### DLP Approved File

![DLP Approved File](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2f31a2be1c78bf84/61683e6c19bdec3c9fc22761/download-screenshot.png)

The DLP `approved` file is not different in any way from today’s user experience. The user is not aware any file scanning has occurred.

### Default Approved File

There is a built-in timer of 10 seconds which will `approve` the file if the DLP system does not respond in time.

![Default Approved File](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta9e1adc3dcd0ee27/61683e6d55bcc83601f7cfee/file-not-scanned.png)

There is an indication to the user that the file was not scanned for sensitive information.

### DLP Rejected File

The following shows the user experience for a file that was `rejected` by the DLP vendor typically due to some policy violation (leaking credit card numbers, PII data etc.).

![DLP Rejected File](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt653c87880ebd2866/61683e6cf748fa3c9d0236fe/blocked-file.png)

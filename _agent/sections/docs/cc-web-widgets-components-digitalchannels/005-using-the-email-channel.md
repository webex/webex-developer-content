---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the Email Channel
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels). [Full Markdown](../../../../docs/cc-web-widgets-components-digitalchannels.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope](002-release-scope.md) [Prerequisites](003-prerequisites.md) [Getting Started](004-getting-started.md)

## Article introduction

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Selected section

## Using the Email Channel

When you receive an email task, the Digital Channels Widget displays the email
interface. This section explains the email features and action buttons available
to you.

### Viewing Your Email List

When you receive an email task, the widget displays a list of all emails in the
conversation thread. Each email entry shows the sender information, timestamp,
status, and a preview of the content.

![Email list view – displays the email conversation thread assigned to the
agent](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt31755d5179e20fa5/69976a1045700700085f50b8/digital-channels-widget-001-email-list-view.png)

| Element           | Description |
| ----------------- | ----------- |
| Task Header       | Shows "Email Task" with a close (×) button |
| Subject Line      | Displays the email subject with a refresh icon |
| Email Entries     | List of individual emails in the thread |
| Sender            | Email address of the sender |
| Timestamp         | Date and time of the email |
| Status Indicator  | Shows "Received" for incoming or "Sent" for outgoing emails |
| Preview Text      | Brief preview of the email content |
| Expand/Collapse   | Chevron icon (∨) to expand or collapse individual emails |

### Reading an Email and Response Options

When you click on an email entry (or the expand arrow), the email expands to
show the full content along with action buttons for responding.

![Email expanded view – shows complete email details with response
options](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta37d05eb1140e6db/69976a101eaffc0008e46086/digital-channels-widget-002-email-expanded-view.png)

**Email header information:**

- **Subject** – Full email subject line
- **From** – Sender's email address
- **Sent** – Full date and time when the email was sent
- **To** – Recipient email address(es)

**Action buttons (displayed at the bottom of the expanded email):**

| Button     | Description |
| ---------- | ----------- |
| Reply      | Respond directly to the sender only |
| Reply All  | Respond to the sender and all recipients in the thread |
| Forward    | Forward the email to another recipient |

**Quick action icons (top-right corner):** Reply, Reply All, Forward, and
Collapse (∧ arrow) to minimize the email.

### Composing and Sending Email Responses

When you click Reply, Reply All, or Forward, the email composer opens so you
can compose and send a response.

![Email reply composer – rich text editor for composing email
responses](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2420158283e72e6e/69976a10b13d650008b4f6c9/digital-channels-widget-010-email-reply-composer.png)

**Composer header:**

- **Subject Line** – Pre-filled with "Re:" prefix for replies
- **Delete Button** – Discard the draft
- **To field** – Recipient (auto-populated for Reply)
- **+ Cc / + Bcc** – Add carbon copy or blind carbon copy recipients

**Rich text formatting toolbar:** Heading, Bold, Italic, Underline, Strikethrough,
text color, numbered list, bullet list, block quote, insert table, insert link,
alignment, attach file, insert template, insert emoji.

**Original email thread:** Displays below a separator with Subject, From, Sent,
and To from the original email.

**Action buttons:** Clear (clears composer content) and Send (sends the email
response).

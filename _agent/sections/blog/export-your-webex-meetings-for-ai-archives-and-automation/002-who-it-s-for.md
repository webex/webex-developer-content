---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Who It's For
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## Who It's For

- **AI enthusiasts** – Feed transcripts and summaries into **Gemini, Claude, ChatGPT, or custom LLMs** for post-meeting analysis, automated follow-ups, or knowledge extraction
- **Compliance teams** – Maintain compliant, searchable archives with local or cloud backups
- **Automation engineers** – Trigger exports programmatically—call `export_meeting()` from Python or use webhooks for zero-touch automation
- **Integration builders** – Extend with new backends (OneDrive, Slack, Dropbox) without touching core logic

It's designed to be simple for quick one-off exports and flexible enough to plug into bigger systems—or your AI assistant's workflow.

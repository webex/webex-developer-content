---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- What It Does
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## What It Does

meetings-exporter pulls together the full picture of your meetings:

- **Meeting details** – Title, date, time, host, and participants
- **Recordings** – Video files (MP4, WebM, M4A) downloaded and saved locally
- **Transcripts** – VTT or plain text, ready for search or analysis
- **AI summaries** – Webex Meeting Summaries API output (summary text + action items)

Each meeting gets its own folder, named like `2026-02-05 14-00 - Project Kickoff`, so everything sorts chronologically and stays easy to find.

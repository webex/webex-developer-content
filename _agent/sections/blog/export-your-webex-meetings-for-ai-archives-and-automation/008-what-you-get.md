---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- What You Get
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## What You Get

Each exported meeting produces a folder like this:

```
2026-02-05 14-00 - Q1 Planning Session/
  meeting_details.txt   # Title, date, host, participants
  transcript.vtt        # Or transcript.txt
  summary.json          # Raw Meeting Summaries API response
  recording_1.mp4       # 45 minutes, 1080p
```

Everything is normalized and ready for downstream tools—or your AI assistant. The `summary.json` gives you the full Meeting Summaries API payload if you want to build custom parsers or integrations.

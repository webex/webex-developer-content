---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Quick Start
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## Quick Start

```bash
git clone https://github.com/WebexSamples/meetings-exporter.git
cd meetings-exporter
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
cp env.template .env
# Edit .env and set WEBEX_ACCESS_TOKEN
```

**List your recent meetings:**

```bash
meetings-exporter list --from 2026-02-01 --to 2026-02-28 --max 10
```

**Export a single meeting to a local folder:**

```bash
meetings-exporter export MEETING_ID --output-dir ./exports
```

**Export all meetings in a date range:**

```bash
meetings-exporter export --from 2026-02-01 --to 2026-02-28 --output-dir ./exports
```

No Google or cloud setup is required for local export—just your Webex token.

**Note:** The Webex APIs have rate limits. When exporting large date ranges, the tool automatically throttles requests. For very large archives (100+ meetings), consider running overnight or in batches.

---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Supercharge Your AI Assistant
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## Supercharge Your AI Assistant

Imagine finishing a meeting and having Gemini, ChatGPT, or Claude instantly ready to:

- **Generate follow-up emails** from the transcript and action items
- **Extract key decisions** and add them to your project tracker
- **Answer questions** like "What did Sarah commit to in last week's meetings?"
- **Create stakeholder summaries** without re-watching recordings
- **Build a searchable knowledge base** across all your team's meetings

With meetings-exporter, your meeting data becomes **AI-ready the moment the meeting ends**. Export to Google Drive, point your AI assistant at the folder, and let it work its magic. No manual downloads, no copy-paste, no switching between tools.

**Example workflow:**
1. Meeting ends → webhook triggers automatic export to Google Drive
2. Gemini reads `transcript.txt` and `summary.txt` from your Drive folder
3. You ask: "What action items came out of this morning's sync?"
4. Gemini responds with a clean list, complete with context and owners

The same workflow works with ChatGPT's file uploads, Claude's Projects feature, or any custom RAG pipeline you build.

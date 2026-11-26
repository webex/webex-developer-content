---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Webhook Server: Auto-Export on Events'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## Webhook Server: Auto-Export on Events

When your meeting ends, Webex POSTs a JSON payload to your webhook server. The tool extracts the meeting ID, acknowledges the event instantly (so Webex doesn't retry), then exports everything in the background—no manual intervention required.

**How it works:**

1. Run `meetings-exporter webhook --port 8080` and expose it via [ngrok](https://ngrok.com) (or another tunnel) so Webex can reach it.
2. Register webhooks with Webex: `meetings-exporter webhook register --url https://your-ngrok-url.ngrok-free.app`
3. When a meeting ends, a recording is created, or a transcript is ready, Webex POSTs to your `/webhook` endpoint.
4. The server responds with 200 immediately, then runs `export_meeting()` in a background thread.
5. The full export runs—meeting details, participants, recordings, transcript, summary—and writes to your configured backend (local folder or Google Drive).

**Events we listen for:**

- `meetings.ended` – Meeting has ended
- `recordings.created` – Recording is available for download
- `meetingTranscripts.created` – Transcript is ready

You can optionally set `WEBEX_WEBHOOK_SECRET` in `.env` to verify the `X-Spark-Signature` header and reject forged requests. When done testing, run `meetings-exporter webhook unregister` to remove the webhooks.

**Troubleshooting Webhooks:**
- **Ngrok URL changes?** Re-run `webhook register` with the new URL
- **Not receiving events?** Check `meetings-exporter webhook list` to verify registration
- **Export failing silently?** Check server logs—background threads don't print errors to console by default. Run with `--log-level DEBUG` for detailed output.

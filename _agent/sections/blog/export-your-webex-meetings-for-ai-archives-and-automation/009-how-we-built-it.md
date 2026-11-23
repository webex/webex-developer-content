---
type: Excerpt
canonical_url: https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- How We Built It
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/export-your-webex-meetings-for-ai-archives-and-automation). [Full Markdown](../../../../blog/export-your-webex-meetings-for-ai-archives-and-automation.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Start](004-before-you-start.md)

## Article introduction

Ever finish a Webex meeting and think, "I wish I could automatically save that recording, transcript, and AI summary somewhere useful"? Maybe you want to feed meeting insights into an LLM, build a searchable company knowledge base, or just keep a clean archive without clicking through the web interface every time.

Today we're open-sourcing **meetings-exporter**—a Python CLI that does exactly that. Export everything from a Webex meeting into a tidy folder structure or straight to Google Drive, ready for your AI assistant to analyze.

## Selected section

## How We Built It

meetings-exporter is built on two Webex API families. Here's what we use and where to find the docs.

### Webex Meetings API

The [Webex Meetings API](https://developer.webex.com/docs/meetings) gives us meeting metadata, participants, recordings, and transcripts. We call these endpoints:

- **[List Meetings](https://developer.webex.com/docs/api/v1/meetings/list-meetings)** – Lists past meetings in a date range. We use `meetingType=meeting` so we only get individual instances (series don't support transcripts or summaries).
- **[Get a Meeting](https://developer.webex.com/docs/api/v1/meetings/get-a-meeting)** – Fetches title, start/end time, host, and other metadata for a single meeting.
- **[List Meeting Participants](https://developer.webex.com/docs/api/v1/meeting-participants/list-meeting-participants)** – Returns attendees with display names and emails for `meeting_details.txt`.
- **[List Recordings](https://developer.webex.com/docs/api/v1/recordings/list-recordings)** – Lists recordings for a meeting (IDs, host email, format).
- **[Get Recording Details](https://developer.webex.com/meeting/docs/api/v1/recordings/get-recording-details)** – Returns `temporaryDirectDownloadLinks.recordingDownloadLink`, a pre-signed CDN URL for the actual video file. We use this (not `downloadUrl`, which points to a web page) to download the MP4/WebM/M4A binary.
- **[Meeting Transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts)** – Lists transcripts for a meeting. We use the `txtDownloadLink` from each item to download the VTT or plain-text content.

### Meeting Summaries API

The [Meeting Summaries API](https://developer.webex.com/meeting/docs/api/v1/meeting-summaries) provides AI-generated summaries and action items:

- **[Get Summary by Meeting ID](https://developer.webex.com/meeting/docs/api/v1/meeting-summaries/get-summary-by-meeting-id)** – Returns the summary text and action items for a meeting. We write the summary to `summary.txt` and the full JSON response to `summary.json`.

### Architecture

We fetch all of this via a single `WebexClient`, normalize it into a `MeetingData` model, and pass it to pluggable exporters (local folder or Google Drive). The design makes it straightforward to add OneDrive, Dropbox, or other backends without changing the ingestion logic.

**⚠️ Important:** Summaries, recordings, and transcripts are available only for **individual meeting instances** (IDs like `abc123_I_xyz789`), not recurring series. Series IDs won't return this data. The tool filters for instances automatically when listing meetings, but if you manually pass a series ID to `export`, the export will be incomplete. Always export instance meetings, not series.

Contributions are welcome—see [CONTRIBUTING.md](https://github.com/WebexSamples/meetings-exporter/blob/main/CONTRIBUTING.md) for setup and code style.

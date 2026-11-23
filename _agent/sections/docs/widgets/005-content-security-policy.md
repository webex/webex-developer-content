---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Content Security Policy
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets). [Full Markdown](../../../../docs/widgets.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Embed the power of Webex in your web applications ✨

## Selected section

## Content Security Policy

Webex Widgets can be used on websites which implement a Content Security Policy (CSP) via the Content-Security-Policy HTTP header.
Consult your webserver's documentation for more information about configuring CSP.
If you're using CSP, use these individual policy directives and their associated values to enable access to the widgets and to allow connectivity to the Webex Platform:

| Policy Directive| Value |
| --- | --- |
| `script-src` | `'self' 'unsafe-inline' https://code.s4d.io;` |
| `style-src` | `'self' 'unsafe-inline' https://code.s4d.io;` |
| `media-src` | `'self' https://code.s4d.io https://*.clouddrive.com https://*.giphy.com https://*.webexcontent.com data: blob:;` |
| `font-src` | `'self' https://code.s4d.io;` |
| `img-src` | `'self' https://*.clouddrive.com https://code.s4d.io https://*.webexcontent.com data: blob: https://*.rackcdn.com;` |
| `connect-src` | `'self' localhost ws://localhost:8000 wss://*.ciscospark.com wss://*.wbx.com wss://*.wbx2.com https://*.ciscospark.com https://*.clouddrive.com/ https://code.s4d.io https://*.giphy.com https://*.wbx2.com https://*.webex.com  https://*.webexcontent.com;` |

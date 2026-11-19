---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-digitalchannels). [Full Markdown](../../../../docs/cc-web-widgets-components-digitalchannels.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope](002-release-scope.md) [Prerequisites](003-prerequisites.md) [Getting Started](004-getting-started.md)

## Article introduction

The Digital Channels Widget provides a unified interface for agents to manage chat, email, and social media customer interactions in Webex Contact Center. It includes built-in messaging controls, email composition tools, and automatic channel detection.

## Selected section

## Troubleshooting

### Widget Not Rendering

**Symptom:** The Digital Channels Widget does not appear.

**Possible causes and solutions:**

| Cause                    | Solution |
| ------------------------ | -------- |
| Widgets not initialized  | Ensure `store.init()` has completed successfully; check console for errors |
| Agent not logged in      | Verify agent has completed Station Login |
| No active digital task   | Widget only renders when there is an active chat, social, or email task |

### Theme Not Applying

**Symptom:** Widget appears but theme is incorrect.

**Solutions:**

- Verify the theme is set in the store using `store.setCurrentTheme('LIGHT')` or
  `store.setCurrentTheme('DARK')`
- Ensure Momentum UI components are properly loaded

### Token or Authentication Errors

**Symptom:** Console shows JWT or token-related errors.

**Solutions:**

- Verify access token is valid and not expired
- Ensure token has required scopes for digital channels
- Check network connectivity to Webex services

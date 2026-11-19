---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- What agents should see
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-participant-drop-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use the existing CallControlCAD widget to remove an eligible participant from an active conference. The Participants menu shows who is on the call, while the current primary agent can use Drop where permitted. This beta guide covers both the React widget and its Web Component wrapper.

## Selected section

## What agents should see

- **Primary agent:** The Participants menu can show the Customer and other supported call participants. Drop is available for eligible Customer, Agent, and joined Entry Point/dial-number (EP-DN) rows. Dropping the Customer requires confirmation; eligible Agent and joined EP-DN rows act immediately.
- **Other agents:** The roster remains visible where eligible, but Drop actions are hidden. Supervisor rows are visible without a Drop action. The primary-agent label and icon follow the call owner reported by Contact Center; the widget does not choose a successor.
- **Before an EP-DN consult joins:** The dialed number may appear in the list while the call is ringing. Its Drop action stays disabled until it becomes a conference participant. An active, non-held consult disables other Drop actions; a held consult can leave established conference targets enabled.
- **While Drop is pending:** All Drop actions are locked until the request completes. The list changes when Contact Center reports the participant leaving, not when the button is first clicked. A failed request shows a generic error. Hosts can register the existing store-level error handler with `store.setOnError((widgetName, error) => { /* handle the error */ })`; the callback receives the widget name and an `Error`. Avoid logging participant identifiers or raw event payloads.
- **As the call changes:** A Customer-only, one-to-one call uses the original call UI. If the Customer leaves but another supported participant remains with the viewing agent, the Participants section stays visible. If the last other participant leaves and only the Customer remains, the roster closes.

The cropped views below show the same menu for the primary agent and a secondary agent. Identifying details are redacted.

![Primary agent participant menu showing Customer and Participants sections with Drop actions; identifying details are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte73fe49ce0e42a71/6ac384469c578226f1d674d8/participant-drop-widgets-primary-menu.png)

*Primary-agent view: eligible Customer and Agent rows have Drop actions.*

![Secondary agent participant menu showing Customer and Participants sections and a Primary marker, without Drop actions; identifying details are redacted.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2a5431a7defaa22b/6ac384999c57821128d6751f/participant-drop-widgets-secondary-menu.png)

*Secondary-agent view: the current owner is marked Primary, and this agent has no Drop actions.*

The backend remains responsible for authorizing and removing participants. Visibility of a Drop button is not an authorization guarantee.

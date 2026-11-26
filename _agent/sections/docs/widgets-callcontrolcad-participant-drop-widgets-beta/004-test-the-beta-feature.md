---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Test the beta feature
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-participant-drop-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use the existing CallControlCAD widget to remove an eligible participant from an active conference. The Participants menu shows who is on the call, while the current primary agent can use Drop where permitted. This beta guide covers both the React widget and its Web Component wrapper.

## Selected section

## Test the beta feature

Test with agents who can join the same voice conference. For each case, note whether you are the primary or a secondary agent and whether a consult is ringing, connected, or held.

| Scenario | Action | Expected result |
| --- | --- | --- |
| Primary and secondary views | Open Participants on both agents' screens. | Both see eligible rows. Only the current primary agent sees enabled Drop actions. |
| Agent Drop | From the primary agent's screen, drop another joined Agent. | The request shows a pending state. After the participant-left update, that Agent disappears; the remaining call stays usable. |
| Customer confirmation | Select Drop for Customer, then Cancel or press Escape. Repeat and confirm. | Cancel/Escape makes no Drop request. Confirm starts Drop, and the Customer row disappears after the reported update. |
| Customer leaves with another Agent present | Have the Customer hang up or be dropped. | Customer disappears; Participants remains for the other Agent. |
| Return to one-to-one | Remove the last other Agent while the Customer remains. | The Participants menu disappears and the original one-to-one call UI remains. |
| EP-DN consult | Dial an Entry Point and observe it before and after a participant answers and joins. | The dialed number can appear before merge with Drop disabled; the joined participant is shown without a duplicate stale EP-DN row. |
| Consult gating | Start a consult, then hold or end it. | An active, non-held consult blocks Drop; eligible established targets become available when the consult is held or ends. |
| Primary agent changes | Have the primary agent leave while two other agents remain. | The new owner receives Drop permission; other agents see the new Primary label and icon after owner-change updates. |
| Nested consult cleanup | While Agent 2 consults Agent 3, have the primary agent drop Agent 2. Repeat while Agent 3 is ringing and after answer. | Check that Agent 2's call UI closes and Agent 3's consult ends. If either remains visible, report the event sequence and timing; do not assume the local button can end another agent's task by itself. |

For a walkthrough, see the [Participant Drop widget sample video](https://app.vidcast.io/share/f5acb405-3a94-459a-93d8-ce931eb20f53). You can also use the [hosted React sample](https://widgets.webex.com/samples-cc-react-app/index.html) if it has the approved beta build.

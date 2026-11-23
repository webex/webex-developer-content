---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-build-and-test
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the customer journey
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-build-and-test). [Full Markdown](../../../../docs/app-hub-build-and-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Continue to submission and customer setup](006-continue-to-submission-and-customer-setup.md)

## Article introduction

Turn your chosen app type into a working customer workflow. Plan the components and permissions, build a small working version, and test setup, everyday use, and recovery before preparing your App Hub submission.

## Selected section

## Verify the customer journey

Record the setup, expected result, and observed result for each check:

| Check | Evidence to capture |
| --- | --- |
| Initial setup | A person with the intended role can follow your instructions and reach a working connection. |
| Main workflow | The app produces the stated customer result in each Webex context you plan to support. |
| Missing access or prerequisites | The app explains what is missing and provides a useful next step. |
| Expired access or interrupted setup | The documented recovery path restores operation without mixing customer connections. |
| Repeated actions or events | Retries do not produce unintended duplicate customer actions. |
| Removal or deauthorization | The app stops using revoked access; your instructions explain any remaining cleanup and data handling. |

Have someone other than the app's developer follow the setup instructions. Fix any step that depends on undocumented knowledge, an administrator session left open, or credentials copied manually during development.

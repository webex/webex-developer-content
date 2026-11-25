---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Existing Guest Issuer Apps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer). [Full Markdown](../../../../docs/guest-issuer.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Issuer applications give guest users temporary access to users within your organization. Guest Issuer app creation has been removed—use [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) for new integrations, or follow [Guest Issuer Migration Guide](https://developer.webex.com/docs/guest-issuer-migration) if you have an existing legacy issuer.

## Selected section

## Existing Guest Issuer Apps

If you already have a Guest Issuer application in [My Webex Apps](https://developer.webex.com/my-apps), it provides a *Guest Issuer ID* and a *Secret*. These two parameters are used to generate guest tokens.

The secret was shown only once when the Guest Issuer application was created. Keep this shared secret safe, as you would with any other sensitive piece of information such as a password. If you need to regenerate the secret for any reason, the prior secret will be immediately invalidated.

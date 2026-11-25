---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Encryption
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-guide). [Full Markdown](../../../../docs/webex-assistant-skills-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](002-requirements.md)

## Article introduction

The [Webex Assistant Skills SDK](https://github.com/cisco/webex-assistant-sdk) is designed to simplify the process of creating a Webex Assistant skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Encryption

Skills require encryption in order to safely send and receive requests. For the encryption to work properly, we need
to provide a key pair and a secret for our Skills. As we saw in the [Simple Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-simple-skill) and
[MindMeld Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-mindmeld-skill) examples above, the keys and secret will be automatically created for us
when we use the SDK to create a template. However, the SDK also has tools to create these manually if needed.

These tools are under the `crypto` section which we'll try next.

### Generating Secrets

Generating a secret is very simple, simply use the `generate-secret` command:

```bash
webex-skills crypto generate-secret
```

A secret will be logged to the terminal, which then you can add to your app.

### Generating Keys

Generating a key pair is very simple, simply use the `generate-keys` command:

```bash
webex-skills crypto generate-keys
```

A key pair will be created.

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ webex-skills crypto generate-keys --help
Usage: webex-skills crypto generate-keys [OPTIONS] [FILEPATH]

  Generate an RSA keypair

Arguments:
  [FILEPATH]  The path where to save the keys created. By default, they get
              created in the current directory.


Options:
  --name TEXT  The name to use for the keys created.  [default: id_rsa]
  --help       Show this message and exit.
```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Remotes
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

## Remotes

This SDK also has the notion of **remotes**. That is, Skills that are already running and even deployed somewhere, but
we still want to be able to test them using the SDK.

The process for using remotes is very simple, we're going to look into that now. We'll use the `remote` section of the
SDK.

Remotes are added automatically for Skills created with this SDK.

### Creating a Remote

You can create a remote by using the `create` command. Let's recreate a remote for a Skill called `echo`:

```bash
webex-skills remote create echo
```

Follow the prompts to create a new remote:

```bash
$ webex-skills remote create echo

Secret: <SECRET>
Public key path [id_rsa.pub]: <KEY_PATH>
URL to invoke the skill [http://localhost:8080/parse]: <URL>
```

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ webex-skills remote create --help

Usage: webex-skills remote create [OPTIONS] NAME

  Add configuration for a new remote skill to the cli config file

Arguments:
  NAME  The name to give to the remote.  [required]

Options:
  -u TEXT            URL of the remote. If not provided it will be requested.
  -s, --secret TEXT  The skill secret. If not provided it will be requested.
  -k, --key PATH     The path to the public key. If not provided it will be
                     requested.

  --help             Show this message and exit.
```

### Listing Remotes

You can also list the remotes you currently have set up. For that you can use the `list` command:

```bash
webex-skills remote list
```

You will get something like:

```bash
{'echo': {'name': 'echo',
          'public_key_path': '<KEY_PATH>',
          'secret': '<SECRET>',
          'url': 'http://localhost:8080/parse'},
 'greeter': {'app_dir': '<APP_DIR>>',
             'name': 'greeter',
             'private_key_path': '<KEY_PATH>',
             'project_path': '<PROJECT_PATH>',
             'public_key_path': '<KEY_PATH>',
             'secret': '<SECRET>',
             'url': 'http://localhost:8080/parse'},
 'switch': {'app_dir': '<APP_DIR>>',
            'name': 'switch',
            'private_key_path': '<KEY_PATH>',
            'project_path': '<PROJECT_PATH>',
            'public_key_path': '<KEY_PATH>',
            'secret': '<SECRET>',
            'url': 'http://localhost:8080/parse'}}
```

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ run webex-skills remote list --help

Usage: webex-skills remote list [OPTIONS]

  List configured remote skills

Options:
  --name TEXT  The name of a particular skill to display.
  --help       Show this message and exit.
```

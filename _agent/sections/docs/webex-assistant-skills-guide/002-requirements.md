---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Requirements
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-guide). [Full Markdown](../../../../docs/webex-assistant-skills-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [Webex Assistant Skills SDK](https://github.com/cisco/webex-assistant-sdk) is designed to simplify the process of creating a Webex Assistant skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Requirements

In order to follow the examples in this guide, we'll need to install the SDK and its dependencies. The SDK works with Python 3.7 and above. Note that if you want to build a **MindMeld skill** as shown later in this guide, you will have to use Python 3.7, which is the highest Python version supported by the **MindMeld Library**.

### Installing the SDK

For this guide, we assume you are familiar and have installed:

- [pyenv](https://github.com/pyenv/pyenv)
- [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
- [pip](https://pypi.org/project/pip/)
- [Poetry](https://python-poetry.org/)

We'll start by creating a virtual environment:

```bash
pyenv install 3.7.5
pyenv virtualenv 3.7.5 webex-skills
pyenv local webex-skills
```

We can now install the SDK using `pip`:

```bash
pip install webex-skills
```

We should be all set, we'll use the SDK later in this guide. You will need to work inside the **webex-skills** virtual
environment we just created.

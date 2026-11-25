---
type: Excerpt
canonical_url: https://developer.webex.com/docs/buttons-and-cards
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What's New
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/buttons-and-cards). [Full Markdown](../../../../docs/buttons-and-cards.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](006-limitations.md)

## Article introduction

Give new levels of interactivity to Webex users by adding Buttons and Cards to your apps.

## Selected section

## What's New

Support for Version 1.3 properties:
* `isRequired`
* `label`
* `errorMessage`
* `regex` 

Sample JSON for card exhibiting input validation using Version 1.3 properties is as follows:
```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.3",
    "body": [
        {
            "type": "Input.Text",
            "label": "Name",
            "isRequired": true,
            "placeholder": "First Name + Last Name",
            "errorMessage": "Please provide a valid input",
            "regex": "^[\\p{L} .'-]+$",
            "id": "sample text"
        },
        {
            "type": "Input.Date",
            "id": "sample date",
            "label": "Date of Birth",
            "errorMessage": "Please enter a valid date",
            "isRequired": true,
            "min": "1960-01-01",
            "max": "1999-12-31"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Action.Submit"
        }
    ]
}

```

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating a Skill
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide). [Full Markdown](../../../../docs/webex-assistant-skills-guide-developer-portal-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Assistant Skills Developer Portal is a tool for skills developers to create and manage their skills' association to the Assistant skills service.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Creating a Skill

To create a skill, click **Create New Skill**:

![Create Skill Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3ccad7234e5d1939/6171b16c5422ab67be73daa5/create_skill_button.png)

You will now be presented with a form that you need to complete in order to create the skill:

![Create Skill Form](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt997216ec8bbba0a0/6171b16cfd37c069473b032a/create_skill_form.png)

The details you need to fill in are the following:

- **Name**: The name of your skill.
- **Description**: An optional description of what this skill does.
- **Home Page**: An optional URL to a website with more information about the skill.
- **Invocation Names**: Keywords that end-users will use to invoke the skill on a Webex Device.
- **Languages**: The list of languages that your skill can support.
- **URL**: URL endpoint to your skill code.
- **Contact Email**: Email of who should be contacted with inquires about the skill. 
- **Secret**: Private string used by the Assistant Service to identify itself to the skill. This string is configured in the application code.
- **Public Key**: A RSA public key needed to securely communicate between the **Assistant skills** Service and the skill.
  
Fill in **all** the fields with your skill details above. When ready, click **OK**.

![Create Skill](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd14f2e024c432144/6171b16c385f7a513f0de935/create_skill.png)

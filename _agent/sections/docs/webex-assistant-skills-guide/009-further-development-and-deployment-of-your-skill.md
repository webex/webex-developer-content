---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Further Development and Deployment of your Skill
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

## Further Development and Deployment of your Skill

Now that your Skill is up and running, you can continue developing and extending its functionality. Furthermore, once the Skill is ready to be tested on **Webex Client** UIs and Webex devices, you can create a Skill entry on the **Assistant Skills** service and begin invoking it. From there, your Webex Admin can choose to enable the Skill for your organization or make it publicly available for other organizations to use.

### Skill Deployment

Once your Skill has reached the point where you would like to be able to test it on devices, you will need to register the Skill. A step-by-step guide on creating and editing your Skill can be found in the [Webex Assistant Skills Developer Portal Guide](https://developer.webex.com/docs/webex-assistant-skills-guide-developer-portal-guide). You will notice when creating a Skill, a URL must be provided. This is so that the **Assistant Skill** service knows where to direct any requests made to the Skill through **Webex Client** UIs and Webex devices.

An important note when registering a Skill created with the Webex Skills SDK is that the Skill will listen for `POST` requests at the `/parse` endpoint. The implementation can be found [here](https://github.com/cisco/webex-assistant-sdk/blob/main/webex_skills/api/base.py#L40).

#### Hosted Skill Deployment

To ensure reliable access and uptime for your Skill, it is recommended that the Skill be deployed to a hosted cloud instance. There are many options available to host your Skill, such as Amazon Web Services, Google Cloud or Microsoft Azure. If available to you, you can use in-house hosting options as well.

You might have noticed that when you create a new Skill, there is a `pyproject.toml` file that gets added to the
project. This file already contains the dependencies needed to run the Skill independently (without using the SDK's
`skills run` command.)

In order to run the Skill independently, you can use [Poetry](https://python-poetry.org/) to manage your dependencies,
or you can also replace the `pyproject.toml` with a `requirements.txt` file if you want to use
[pip](https://pypi.org/project/pip/) instead.

For deployment, the SDK builds the Skill based on [FastAPI](https://fastapi.tiangolo.com/), which offers multiple
options for running an app in production. You can find more information in their
[Deployment Documentation](https://fastapi.tiangolo.com/deployment/).

#### Locally Run Deployment

For testing purposes, you can use tools such as [ngrok](https://ngrok.com/) or [localtunnel](https://github.com/localtunnel/localtunnel) to make your locally running Skill accessible to the **Assistant Skills** service. These tools allow requests made from the **Webex Client** UIs and Webex devices to reach you local Skill and test out your Skill without having to fully deploy your Skill.

### Skill Testing

Earlier in the guide, you tested the Skill via the CLI tools made available through the Webex Skills SDK. This is a useful tool to query your skill and see the returned directives, but now we need to use voice. 

On these interfaces, you can use your voice to invoke and test your skill. Remember you will need to use the skill invocation pattern to reach your skill. The pattern follows a structure like `Ok Webex, tell <Skill Name> <command>`, or `Ok Webex, ask <Skill Name> to <command>`. Make sure the skill is accessible to the internet for this to work. 

#### Webex Assistant Web Tool

One tool made available to test your Skill is the Webex Assistant Web Tool: https://assistant-web.intelligence.webex.com/. This is a browser based tool (developed on Google Chrome) that allows you to use voice, as well as text, to invoke the Webex Assistant.

Login to the interface with the same account used to create the skill in the skills developer portal:
![login Button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt22abf4f9837a3129/61bb8dd7516b317e91fefa02/testing_skill_login.png)

Select the language to enunciate and test the skill commands:
![Select Language](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1c63d3a3a23ec5c9/61bb8dd7abe5293e65780d60/testing_skill_select_language.png)

Click the microphone button to enunciate in chosen language with the skill command:
![Speak the Skill command](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt790bcf9a68049d63/61bb8dd7c52c5b292ce235bb/testing_skill_echo_turn_1.png)

Test the skill responses:
![Skill performs action](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltee8d03b6c963f44e/61bb8dd78c8e757c1a012650/testing_skill_echo_turn_2.png)
![Speak another Skill command](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc641ec259396dc29/61bb8dd73d2b1760404ecb48/testing_skill_echo_turn_3.png)
![Skill performs another action](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt97b458b6609e9a09/61bb8dd78d6b4f214f469e85/testing_skill_echo_turn_4.png)

#### Webex Devices

Users associated with a Control Hub organization can test on a device registered to that organization if the following criteria are met: 

* Webex Assistant for Devices is enabled for the organization
* The user has access to an Assistant supported device that is registered to Control Hub (cloud aware) in personal-mode 
* The skills developer portal integration is not blocked for the organization

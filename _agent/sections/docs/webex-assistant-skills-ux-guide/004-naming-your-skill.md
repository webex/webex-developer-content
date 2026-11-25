---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Naming Your Skill
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-ux-guide). [Full Markdown](../../../../docs/webex-assistant-skills-ux-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

As the developer, Webex Assistant Skills empower you to provide your users with even more voice functionality. In this guide you'll learn about the the high-level ways users will interact with your skill: starting a conversation, continuing a conversation, and ending a conversation.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Naming Your Skill

Your skill's name needs to work consistently in the system while being memorable and intuitive for your users.

### Branding

Choose a skill name that your users will associate with your skill's functionality and your workplace's positive traits. For example, a skill that provides information about your facilities probably shouldn't be named "Gladys" or "Company Bot." Neither of these indicate what service is provided. For some people "Gladys" could be confused with the malevolent AI GLaDOS, while "Bot" is associated with unhelpful automation.

Names like "Help Desk" or "Office Manager" clearly communicate the skill's role and scope. Depending on your design preference, the name can make the skill sound more lifelike (e.g., "Bartleby," "Electra"), moderately lifelike (e.g. "Office Manager," "Meeting Roomba") or more institutional (e.g., "Weather," "Human Resources").

### Speech Recognition

The speech recognition engine should be able to consistently transcribe your skill name. Common alternate spellings can be added as skill name synonyms, but might not be desired for branding reasons.
Brand names that aren't found in the dictionary generally won't work well. If you name your skill "Deskly" or "Weatherator," for example, the speech recognition won't write it that way and will likely alternate between different spellings.

It's helpful to try out the skill names you're considering in the context of the full invocation phrase. For example, if the skill name is "Vision," when a user says "OK Webex, tell Vision to start the coffeemaker," the speech recognition may transcribe it as "television." If the skill name is "Orbit," the speech recognition may transcribe "ask Orbit" as "ascorbic."

Try getting a few people with different accents to speak the invocation phrase to Webex Assistant to verify that the invocation phrase is usually written correctly. Once your skill name is registered, it will be added to the context phrases for the speech recognition within the organization, which will improve the accuracy. Still, a good skill name should typically work even without that.
If you plan to make the skill support multiple languages, you should also consider if the skill name will be recognized in each of the supported languages. Separate skill names for each language are acceptable, but may be undesirable.

### Length and Frequency

Finally, the skill name shouldn't be too long, too common, or too rare.

For skill names that are common and short, there is some risk that a user would invoke it by accident. For example, if the skill is named "B" or "Tom," a user could say "talk to Bea" or "tell Tom to create a ticket," intending to use a core Webex Assistant feature, and your skill would appear instead.

Skill names that are long and uncommon will result in a lot of alternate spellings. Users may find it annoying to say the whole name each time, and a long name will crowd the on-screen hints and replies. To limit complexity, skill names and synonyms should be less than three words long as spelled by the speech recognition engine. For visual simplicity, we recommend that skill names be less than 25 characters..

---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Converting a Simple Skill into a MindMeld Skill
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

## Converting a Simple Skill into a MindMeld Skill

As you are starting your skill creation journey, you'll probably start with a **simple skill**, and as your comfort and the complexity of your skill grows, you might need to convert it into a **MindMeld skill**. The SDK makes that conversion very easy. We are
going to take a look into that next.

Consider the [Switch skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-simple-skill) we built above. It really just recognizes if we want to turn something on or off, but what if we have multiple lights? We could, in principle, look at the query and try to extract the light we want to switch with another regex, but that can be very brittle. Instead, let's try turning it into a **MindMeld skill**.

### Adding the Training Data

Let's start by creating our domains, intents and entities. We still want to just turn on and off lights, but we want to
be able to identify which light to switch. On the `switch` app, create the following folder structure:

![File Structure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt677b715140af6bbb/61730e78923218529eecead1/smart_lights_directory.png)

As you can see, we have created a `greeting` and `smart_lights` domains, the intents `greet`, `turn_lights_on`
and `turn_lights_off`, and the entities `all` and `location`. We now need to add training data to make this setup work.

Normally, you would need to collect training data manually to create your domain, intents and entities. But, for this
guide, we are going to take a shortcut. If you are familiar with the [MindMeld library](https://www.mindmeld.com/), you
have probably seen that it comes with **Blueprint** applications, so we are going to borrow some data from one of them.

Go to this [repo](https://github.com/CiscoDevNet/mindmeld-blueprints/tree/develop/blueprints/home_assistant/domains)
and copy the `train.txt` files from the corresponding intents into our folders. Do the same for entities, from 
[here](https://github.com/CiscoDevNet/mindmeld-blueprints/tree/develop/blueprints/home_assistant/entities) copy the 
corresponding `gazetteer.txt` and `mapping.json` files into our folders. Our directory should now look like this:

![File Structure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9b1fd277d58a0cd2/61730e7852c42c67c026d99f/smart_lights_dir_complete.png)

### Updating the Handlers

The next thing we'll do is to convert our logic to turn it into a **MindMeld skill**. The steps are very simple. Let's
start by making all the following changes in `main.py`:

Instead of making the variable `app` a `SimpleApi`, make it a `MindMeldAPI`:

```python
api = MindmeldAPI()
```

In the `@api.handle` decorators, add the intent you want to handle instead of the pattern:

```python
@api.handle(intent='turn_lights_on')
async def turn_on(current_state: DialogueState, processed_query: ProcessedQuery) -> DialogueState:
...

@api.handle(intent='turn_lights_off')
async def turn_off(current_state: DialogueState, processed_query: ProcessedQuery) -> DialogueState:
```

Finally, add some logic to complement the response with the location entity if available. In the `turn_on` handler, 
replace the line:

```python
    text = 'Ok, turning lights on.'
```

With the following logic:

```python
    if len(processed_query.entities) > 0:
        entity = processed_query.entities[0]
        if entity['type'] == 'location':
            text = f'Ok, turning the {entity["text"]} lights on.'
        else:
            text = 'Ok, turning all lights on.'
    else:
        text = 'Ok, turning all lights on.'
```

Do the corresponding change to the `turn_off` handler.

You will also need to import the new classes you are using: `MindmeldAPI` and `ProcessedQuery`.

That's it! We now have NLP support in our Skill. 

All in all your `main.py` should look like this:

```python
from webex_skills.api import MindmeldAPI
from webex_skills.dialogue import responses
from webex_skills.models.mindmeld import DialogueState, ProcessedQuery

api = MindmeldAPI()


@api.handle(default=True)
async def greet(current_state: DialogueState) -> DialogueState:
    text = 'Hello I am a super simple skill'
    new_state = current_state.copy()

    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),
        responses.Sleep(10),
    ]

    return new_state


@api.handle(intent='turn_lights_on')
async def turn_on(current_state: DialogueState, processed_query: ProcessedQuery) -> DialogueState:
    new_state = current_state.copy()

    if len(processed_query.entities) > 0:
        entity = processed_query.entities[0]
        if entity['type'] == 'location':
            text = f'Ok, turning the {entity["text"]} lights on.'
        else:
            text = 'Ok, turning all lights on.'
    else:
        text = 'Ok, turning all lights on.'

    # Call lights API to turn on your light here.

    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),
        responses.Sleep(10),
    ]

    return new_state


@api.handle(intent='turn_lights_off')
async def turn_off(current_state: DialogueState, processed_query: ProcessedQuery) -> DialogueState:
    new_state = current_state.copy()

    if len(processed_query.entities) > 0:
        entity = processed_query.entities[0]
        if entity['type'] == 'location':
            text = f'Ok, turning the {entity["text"]} lights off.'
        else:
            text = 'Ok, turning all lights off.'
    else:
        text = 'Ok, turning all lights off.'

    # Call lights API to turn off your light here.

    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),
        responses.Sleep(10),
    ]

    return new_state
```

### Adding the Parsers Configuration File

One last step we need is to add a config file needed by some parsers. This is added automatically when directly
creating a `MindMeld Skill`, so we'll need to add it manually in this case.

In the `switch` module directory, create a `config.py` file with the following content:

```python
NLP_CONFIG = {'system_entity_recognizer': {}}
ENTITY_RESOLVER_CONFIG = {'model_type': 'exact_match'}
```

### Testing the Skill

We can now test the Skill to make sure it works as intended. Since we just added our training data, we need to build
the models first. Since we have entities defined, we will need to have Elasticsearch running for the `nlp build`
command to work properly. You can refer to the 
[MindMeld Getting Started Documentation](https://www.mindmeld.com/docs/userguide/getting_started.html) for a guide on
how to install and run Elasticsearch.

Remember that in order to build `MindMeld` skills, we need the extra `mindmeld` dependency:

```bash
pip install "webex-skills[mindmeld]"
```

With that out of the way, you can build the models:

```bash
webex-skills nlp build switch
```

We can now run our new Skill:

```bash
webex-skills skills run switch
```

Finally, we can use the `invoke` method to send a couple commands:

```bash
$ webex-skills skills invoke switch
Enter commands below (Ctl+C to exit)
>> hi
{ 'challenge': 'bd57973f82227c37fdaed9404f86be521ecdbefc684e15319f0d51bbecbb456e',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Hello I am a super simple skill'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Hello I am a super simple skill'}, 'type': 'action'},
                  {'name': 'sleep', 'payload': {'delay': 10}, 'type': 'action'}],
  'frame': {},
  'history': [ { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'hi'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634934720}}
>> turn on the lights
{ 'challenge': 'ff8e57bcb94b90c736e11dd79ae5fe3b269dcc450d7bb07b083de73d9a22d5e8',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Ok, turning all lights on.'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Ok, turning all lights on.'}, 'type': 'action'},
                  {'name': 'sleep', 'payload': {'delay': 10}, 'type': 'action'}],
  'frame': {},
  'history': [ { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'hi'},
               { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'turn on the lights'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634934720}}
>> turn off the kitchen lights
{ 'challenge': '300e7adfe2f199998f152793b944bc597c5145e991dda621e1495e2e06cebb6e',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Ok, turning the kitchen lights off.'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Ok, turning the kitchen lights off.'}, 'type': 'action'},
                  {'name': 'sleep', 'payload': {'delay': 10}, 'type': 'action'}],
  'frame': {},
  'history': [ { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'hi'},
               { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'turn on the lights'},
               { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'turn off the kitchen lights'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634934720}}
>> turn off all the lights
{ 'challenge': 'e92a90c304c9ef96a3edf31c6ffb10606739cdf98ad34cfd57314b20138ad59b',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Ok, turning all lights off.'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Ok, turning all lights off.'}, 'type': 'action'},
                  {'name': 'sleep', 'payload': {'delay': 10}, 'type': 'action'}],
  'frame': {},
  'history': [ { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'hi'},
               { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'turn on the lights'},
               { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'turn off the kitchen lights'},
               { 'context': {},
                 'directives': [],
                 'frame': {},
                 'history': [],
                 'params': { 'allowed_intents': [],
                             'dynamic_resource': {},
                             'language': 'en',
                             'locale': None,
                             'target_dialogue_state': None,
                             'time_zone': 'UTC',
                             'timestamp': 1634934720},
                 'text': 'turn off all the lights'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634934720}}
>>
```

We have now converted a **Simple Skill** into a **MindMeld Skill**.

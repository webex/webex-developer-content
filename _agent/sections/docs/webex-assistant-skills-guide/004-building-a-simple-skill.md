---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Building a Simple Skill
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

## Building a Simple Skill

Let's now use the SDK to build a **simple skill**. As mentioned in the example above, we'll build a skill to turn lights on and off according to what the user is asking. We are going to call this skill **Switch**.

### Create the skill from a template

The Webex Assistant Skills SDK provides a CLI tool that makes creating and working with skills easier. To begin,
it can create a simple or MindMeld skill from a provided template.

The command to create a skill is `project init`.

If you run `webex-skills project init --help`, you should see output similar to the below.
```bash
$ webex-skills project init --help
Usage: webex-skills project init [OPTIONS] SKILL_NAME

  Create a new skill project from a template

Arguments:
  SKILL_NAME  The name of the skill you want to create  [required]

Options:
  --skill-path DIRECTORY      Directory in which to initialize a skill project
                              [default: .]

  --secret TEXT               A secret for encryption. If not provided, one
                              will be generated automatically.

  --mindmeld / --no-mindmeld  If flag set, a MindMeld app will be created,
                              otherwise it defaults to a simple app  [default:
                              False]

  --help                      Show this message and exit.
```

The only requirement is that you give your skill a name. With no other options the init command will generate
a new simple skill in the current directory, generate keys for encryption, a shared secret for signing messages
and a basic python project for your Skill code.

Running 
```bash
webex-skills project init switch
```

Should produce a directory structure like this:

![File Structure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdfeffc10c4d226ce/61730e78fd37c069473b07c4/switch_directory.png)

### Configuring a Skill

A skill can be configured in several ways, in code, in the environment or in an environment file. The `init` command creates an environment file for you (the `.env` file shown above) and fills in some default values:

```bash
$ cat switch/.env
SKILLS_SKILL_NAME=switch
SKILLS_SECRET=<randomly generated secret>
SKILLS_USE_ENCRYPTION=1
SKILLS_APP_DIR=<full path to the application directory>
SKILLS_PRIVATE_KEY_PATH=<full path to the private key>
```

The `SKILLS_SECRET` will be used when associating your skill code with Webex. The `PRIVATE_KEY_PATH` is used by the skill to decrypt messages sent by the **Assistant skills** service. In the subsequent sections, you'll see how to run a skill locally and make requests against it using the CLI. To ease development and testing, it is possible to disable encryption by setting `SKILLS_USE_ENCRYPTION=0` in the `.env` file.

### Running the Template

We can now run our skill and start testing it. There are a couple ways you can run it. 

First, this SDK has a `run` command and you can run it as follows:

```bash
webex-skills skills run switch
```

You should see an output similar to:

```bash
INFO:     Started server process [86661]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://127.0.0.1:8080 (Press CTRL+C to quit)
```

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ webex-skills skills run --help
Usage: webex-skills skills run [OPTIONS] SKILL_NAME

Arguments:
  SKILL_NAME  The name of the skill to run.  [required]

Options:
  --help  Show this message and exit.
```

The second option to run a skill is to use `uvicorn`. After all, the skill created is an `asgi` application based on
[FastAPI](https://fastapi.tiangolo.com/):

```bash
uvicorn switch.main:api --port 8080 --reload
```

You should see an output similar to the following:

```bash
INFO:     Will watch for changes in these directories: ['<PATH_TO_SKILL>']
INFO:     Uvicorn running on http://127.0.0.1:8080 (Press CTRL+C to quit)
INFO:     Started reloader process [86234] using statreload
INFO:     Started server process [86253]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

Now that we have the skill running, we can test it.

### Checking the Skill

One quick verification step that we can do before sending requests to the skill code is to make sure we have everything correctly setup. The Webex Skills SDK provides a tool for that. We can call it as:

```bash
webex-skills skills check switch
```

In your skill output, you should see something like this:

```bash
INFO:     127.0.0.1:58112 - "GET /check?signature=<SIGNATURE%3D&message=<MESSAGE>%3D HTTP/1.1" 200 OK
```

In the SDK output, you should see:

```bash
switch appears to be working correctly
```

That means that your skill is running and the `check` request was successfully processed.

### Invoking the Skill for Testing

The SDK `skills` section has an `invoke` command which is used for sending requests to the skill. With the skill
running, we can invoke the skill in a different terminal as follows:

```bash
webex-skills skills invoke switch
```

By default, this makes POST requests and passed commands to `http://localhost:8080/parse` along with some required metadata. If you have changed the default path or host value be sure to update the `remote` entry for this skill 
(see [this section](https://developer.webex.com/docs/webex-assistant-skills-guide#remotes)).

We can now enter a command and see a response:

```bash
$ webex-skills skills invoke switch
Enter commands below (Ctl+C to exit)
>> hi
{ 'challenge': 'a129d633075c9c227cc4bdcd1653b063b6dfe613ca50355fa84e852dde4b198f',
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
                             'timestamp': 1634881359},
                 'text': 'hi'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634881359}}
```

We can see that we got all the directives back. The template skill will simply respond with a greeting.

As usual, you can use the `--help` option to see the documentation for this command:

```bash
$ webex-skills skills invoke --help
Usage: webex-skills skills invoke [OPTIONS] [NAME]

  Invoke a skill running locally or remotely

Arguments:
  [NAME]  The name of the skill to invoke. If none specified, you would need
          to at least provide the `public_key_path` and `secret`. If
          specified, all following configuration (keys, secret, url, ect.)
          will be extracted from the skill.


Options:
  -s, --secret TEXT         The secret for the skill. If none provided you
                            will be asked for it.

  -k, --key PATH            The path of the public key for the skill.
  -u TEXT                   The public url for the skill.
  -v                        Set this flag to get a more verbose output.
  --encrypt / --no-encrypt  Flag to specify if the skill is using encryption.
                            [default: True]

  --help                    Show this message and exit.
```

### Updating the Skill

Let's now modify our skill to understand the inputs to turn on and off the office lights. 

Simply update the `main.py` file with the following two handlers:

```python
@api.handle(pattern=r'.*\son\s?.*')
async def turn_on(current_state: DialogueState) -> DialogueState:
    new_state = current_state.copy()

    text = 'Ok, turning lights on.'
    
      # Call lights API to turn on your light here.
    
    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),
        responses.Sleep(10),
    ]

    return new_state


@api.handle(pattern=r'.*\soff\s?.*')
async def turn_off(current_state: DialogueState) -> DialogueState:
    new_state = current_state.copy()

    text = 'Ok, turning lights off.'
    
    # Call lights API to turn off your light here.
    
    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),
        responses.Sleep(10),
    ]

    return new_state
```

The SDK provides the `@api.handle` decorator, and as you can see, it can take a `pattern` parameter, which is then
applied to the query to determine if the handler should process it. This way, we can add
a few handlers by simple creating regexes that match the type of queries we want to support.

In the example above, we have added regexes to identify the `on` and `off` keywords, which mostly tell what the user
wants to do.

By using the `skills invoke` command, we can run a few tests. 

```bash
>> turn on the lights
{ 'challenge': '56094568e18c66cb89eca8eb092cc3bbddcd64b4c0442300cfbe9af67183e260',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Ok, turning lights on.'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Ok, turning lights on.'}, 'type': 'action'},
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
                             'timestamp': 1634881502},
                 'text': 'turn on the lights'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634881502}}
>> turn off the lights
{ 'challenge': '2587110a9c97ebf9ce435412c0ea6154eaef80f384ac829cbdc679db483e5beb',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Ok, turning lights off.'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Ok, turning lights off.'}, 'type': 'action'},
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
                             'timestamp': 1634881502},
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
                             'timestamp': 1634881502},
                 'text': 'turn off the lights'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634881502}}
>> turn the lights on
{ 'challenge': 'ce24a510f6a7025ac5e4cc51b082483bdbcda31836e2c3567780c231e5674c59',
  'directives': [ {'name': 'reply', 'payload': {'text': 'Ok, turning lights on.'}, 'type': 'action'},
                  {'name': 'speak', 'payload': {'text': 'Ok, turning lights on.'}, 'type': 'action'},
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
                             'timestamp': 1634881502},
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
                             'timestamp': 1634881502},
                 'text': 'turn off the lights'},
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
                             'timestamp': 1634881502},
                 'text': 'turn the lights on'}],
  'params': { 'allowed_intents': [],
              'dynamic_resource': {},
              'language': 'en',
              'locale': None,
              'target_dialogue_state': None,
              'time_zone': 'UTC',
              'timestamp': 1634881502}}
```

In the examples above, we see the skill responding with the correct message. For the production skill, we would also call an API on our backend to perform the action of turning on or off the lights.

### More About the Simple Skill Handler Signature

When we created our **simple skill**, our handler had the following signature:

```python
async def greet(current_state: DialogueState) -> DialogueState:
```

You can also update the handler to give you another parameter:

```python
async def greet(current_state: DialogueState, query: str) -> DialogueState:
```

The `query` string parameter will give you the query that was sent to the skill, this can be used in cases where you
need to further analyze the text.

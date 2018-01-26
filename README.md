<img src='https://raw.githubusercontent.com/botpress/botpress-nlu/master/assets/banner_demo.gif'>

# Botpress NLU ⚡

Botpress NLU is a Botpress module that adds NLU capatibilities to your bot by connecting to the NLU provider of your choice.

**🚧 I'm looking for help to support more providers**

| Provider | 🚩 Status |
| ------------- | :--------: |
| [LUIS](https://www.luis.ai) | ✅ |
| [DialogFlow](https://dialogflow.com/) | Help needed |
| [RASA](https://github.com/RasaHQ/rasa_nlu) | Help needed |

We believe NLP/NLU is a commodity, so this package abstracts the provider by providing a standard, clean interface that allows you (and the non-technicals) to easily edit the NLU data within Botpress. We are building the **interface** for proper NLU, we are **NOT** involved in actually providing the NLU.

With Botpress NLU,

- You own your data
- You can seamlessly switch to another NLP provider
- _(soon)_ You can continously train your bot on misunderstood phrases
- _(soon)_ You can share and import open-source, community-curated intents & entities

# Installation

⚠️ **This module only works with the upcoming [Botpress X](https://github.com/botpress/botpress/tree/develop/x).**

- Install the module `yarn add botpress-nlu`
- Configure a provider (see below)

# Standard NLU Object (`event.nlu`)

Botpress NLU will instrument incoming events by providing a standardized object with the structure below.

| Path | Description | Supported by |
| ---- | ----------- | ---- |
| `nlu.intent.name` | The name of the classified intent | LUIS |
| `nlu.intent.confidence` | Confidence of the classification, between `0` and `1`, higher the better | LUIS |
| `nlu.intent.provider` | The provider that provided the classification | LUIS |
| `nlu.entities[i].name` | The name of the extracted entitiy | - |
| `nlu.entities[i].type` | The type of entity that was extracted | LUIS |
| `nlu.entities[i].value` | The **normalized** value of the extracted entity | LUIS |
| `nlu.entities[i].original` | The original (raw) value of the extracted entity | - |
| `nlu.entities[i].confidence` | The provider that extracted the entity | LUIS |
| `nlu.entities[i].position` | The position where it was found in the input string (start position) | LUIS |
| `nlu.sentiment` | TBD | - |
| `nlu.language` | TBD | - |

## LUIS

### LUIS Configuration [(source)](https://github.com/botpress/botpress-nlu/blob/master/src/index.js#L14-L23)

| Key | Environment Variable | Required |
| ------------- | -------- | ----- |
| luisAppId | `NLU_LUIS_APP_ID` | Yes |
| [luisProgrammaticKey](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/manage-keys) | `NLU_LUIS_PROGRAMMATIC_KEY` | Yes |
| luisAppSecret | `NLU_LUIS_APP_SECRET` | Yes |
| luisAppRegion | `NLU_LUIS_APP_REGION` | No (default is `westus`) |

### LUIS Caveats

There are some entities that LUIS doesn't support in some languages, make sure that the language you are using supports the entities you are using in Botpress (this module doesn't do this check for you).

### LUIS FAQ

<details>
  <summary><strong>I get an error when syncing my model</strong> <i>(click to see)</i></summary>
  Make sure that:
  
  - You have enough labels (min 2) for the intent
  - The entities you are using are supported by your app's language
</details>

# Contributing

The best way to help right now is by helping with the exising issues here on GitHub and by reporting new issues!

# License

Botpress is dual-licensed under [AGPLv3](/licenses/LICENSE_AGPL3) and the [Botpress Proprietary License](/licenses/LICENSE_BOTPRESS).

By default, any bot created with Botpress is licensed under AGPLv3, but you may change to the Botpress License from within your bot's web interface in a few clicks.

For more information about how the dual-license works and why it works that way please see the <a href="https://botpress.io/faq">FAQS</a>.



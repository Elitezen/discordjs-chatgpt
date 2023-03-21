# discordjs-chatgpt

![screenshot](https://i.imgur.com/Ye0BWpW.png)

A small module for quick implemntation of OpenAI's Chat-GPT into Discord.JS. This is the first public version of the library. For bug reports or feature requests visit https://github.com/Elitezen/discordjs-chatgpt

This module requires an OpenAI API key. You can get one [here](https://platform.openai.com/account/api-keys)

---
# Updates
## 0.2.0

Added `ChatGPTClient.forgetContext()`

---

**Installing**

```ssh
npm i discordjs-chatgpt
```

## Example Usage

### Interaction

```js
const { SlashCommandBuilder } = require('discord.js');

const { ChatGPTClient } = require('discordjs-chatgpt');
const chatgpt = new ChatGPTClient('YOUR_OPENAI_API_KEY');

module.exports = {
  data: new SlashCommandBuilder()
    .setName('chatgpt')
    .setDescription('Talk with Chat-GPT!')
    .addStringOption(option =>
        option
          .setName('message')
          .setDescription('Your message')),
  async execute(interaction) {
      const msg = interaction.options.getString('message', true);
      await chatgpt.chatInteraction(interaction, msg);
  }
};
```

### Message

Filter messages and clean `message.content` as needed.

```js
const { Events } = require('discord.js');

const { ChatGPTClient } = require('discordjs-chatgpt');
const chatgpt = new ChatGPTClient('YOUR_OPENAI_API_KEY');

const examplePrefix = "!";

module.exports = {
	name: Events.MessageCreate,
	once: false,
	execute(message) {
        const msg = message.content.replace(examplePrefix, '');
		return await chatgpt.chatMessage(message, msg);
	},
};
```

## Options

You can toggle context remebering, and response type.

```js
const chatgpt = new ChatGPTClient('YOUR_OPENAI_API_KEY', {
  contextRemembering: true,
  responseType: 'embed' // or 'string'
});
```
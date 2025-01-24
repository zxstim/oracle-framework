# oracle framework

Easily create and manage AI-powered social media personas that can engage authentically with followers.

## Overview

Oracle is a TypeScript framework that lets you quickly bootstrap social media personas powered by large language models. Each persona has its own personality, posting style, and interaction patterns.

## Quick Start

1. Clone and install dependencies:

```bash
git clone git@github.com:teeasma/oracle-framework.git
cd oracle-framework
npm install
# or with yarn
yarn install
```

2. Set up environment:

```bash
cp .env.example .env
```

3. Configure your `.env` file with:

- LLM provider credentials (OpenRouter recommended)
- Twitter account credentials
- Telegram bot token (optional)

4. Create your agent:

- Copy and modify `src/characters/characters.json` with your agent's personality. You can have more than one agent in the file but that is advanced usage.

5. Run:

```bash
# Generate Twitter authentication
npm run dev -- generateCookies <username>
# or with yarn
yarn dev generateCookies <username>

# Start the agent's actions on Twitter
npm run dev -- autoResponder <username>     # Reply to timeline
npm run dev -- topicPost <username>         # Post new topics
npm run dev -- replyToMentions <username>   # Handle mentions

# Start the agent's actions on Telegram
npm run dev telegram <username>

# Start the agent's actions on Discord
npm run dev discord <username>
```

## Development

```bash
# Build the project
npm run build
# or
yarn build

# Run in development mode
npm run dev
# or
yarn dev

# Format code
npm run format
# or
yarn format
```

## Features

- **AI-Powered Interactions**: Uses LLMs to generate human-like responses and posts
- **Personality System**: Define your agent's character, tone, and behavior
- **Multi-Modal**: Can generate and handle text, images, and voice content
- **Platform Support**: Supports Twitter, Telegram, Discord and more integrations coming soon
- **Engagement Tools**: Auto-posting, replies, mention handling

## Configuration

### Character Setup

Characters are defined in JSON files under `src/characters/`. Each character file contains the AI agent's personality, behavior patterns, and platform-specific settings.

Create a new JSON file in `src/characters/` with the following structure:

```json
{
  "agentName": "Display Name",
  "username": "handle",
  "bio": ["Multiple bio options"],
  "lore": ["Background stories and history", "Helps establish character depth"],
  "postDirections": [
    "Guidelines for posting style",
    "Tone and voice instructions"
  ],
  "topics": ["Subjects the agent discusses", "Areas of expertise or interest"],
  "adjectives": [
    "used for post generation",
    "i.e. generate a 'cute' post about the agent's favorite topic"
  ],
  "postingBehavior": {
    "replyInterval": 2700000,
    "topicInterval": 10800000,
    "removePeriods": true,
    "chatModeRules": ["Custom response rules for Telegram"]
  },
  "model": "anthropic/claude-3.5-sonnet",
  "fallbackModel": "meta-llama/llama-3.3-70b-instruct",
  "temperature": 0.75
}
```

#### Key Configuration Fields:

- **agentName**: Display name shown on social platforms
- **username**: Twitter handle without '@'
- **bio**: The agent's bio
- **lore**: Background stories that shape the character's history
- **postDirections**: Guidelines for how the agent should post
- **topics**: Subjects the agent is knowledgeable about
- **adjectives**: Character traits that define the personality
- **postingBehavior**: Technical settings for posting frequency and style
- **model**: Primary LLM to use for generation
- **temperature**: "Creativity" level - 0.0-1.0, higher = more creative. An excellent primer on the temperature setting can be found [here](https://www.vellum.ai/llm-parameters/temperature).

For a complete example, check out `src/characters/carolaine.json`. You can see her in action at [@carolainetrades](https://twitter.com/carolainetrades).

#### Platform-Specific Settings

You can also configure platform-specific behavior:

```json
{
  "telegramBotUsername": "YOUR_BOT_USERNAME",
  "chatModeRules": ["Custom response patterns"],
  "imageGenerationBehavior": {
    "provider": "ms2",
    "imageGenerationPromptModel": "meta-llama/llama-3.3-70b-instruct"
  },
  "voiceBehavior": {
    "voice": "voice_id"
  }
}
```

### Environment Variables

Required variables in `.env`:

```
LLM_PROVIDER_URL=
LLM_API_KEY=

# Twitter configuration (if using Twitter)
AGENT_TWITTER_PASSWORD=

# Telegram configuration (if using Telegram)
AGENT_TELEGRAM_API_KEY=

# Discord configuration (if using Discord)
AGENT_DISCORD_API_KEY=

# MS2 configuration (if using MS2 for image generation)
AGENT_MS2_API_KEY=
```

## Commands

### Twitter

- `generateCookies`: Create Twitter authentication cookies
- `autoResponder`: Start the timeline response system
- `topicPost`: Begin posting original content
- `replyToMentions`: Handle mentions and replies

### Telegram

- `telegram`: Start the Telegram bot

Important:

- Telegram requires a bot token, which you can get from [@BotFather](https://t.me/botfather) in Telegram.

### Discord

- `discord`: Start the Discord bot

Important:

- Discord requires an API key, which you can get from [the Discord Developer Portal](https://discord.com/developers/applications)

## LLM Providers

- **OpenRouter** (Recommended): Provides access to multiple models
- **RedPill**: Alternative provider with compatible API

## Best Practices

1. Test your agent's personality thoroughly before deployment
2. Monitor early interactions to ensure appropriate responses
3. Adjust posting frequencies based on engagement
4. Regularly update the agent's knowledge and interests

## Development Status

Current TODO:

- [ ] Improve reply quality on Twitter
- [ ] Add scraping of targeted content
- [ ] Develop reply prioritization system

## Support

For issues and feature requests, please use the GitHub issue tracker.

# Discord Handler JavaScript

A modern, feature-rich Discord bot handler built with **Discord.js v14**, featuring both slash commands and prefix commands with a robust modular architecture designed for scalability and maintainability.

## Features

- **Dual Command System**: Support for both slash commands and prefix commands
- **Modular Architecture**: Clean separation of concerns with dedicated handlers
- **Anti-Crash System**: Comprehensive error handling and monitoring
- **Event-Driven**: Fully event-driven architecture
- **Webhook Logging**: Real-time logging for errors and guild events
- **MongoDB Integration**: Persistent data storage with Mongoose
- **Cooldown System**: Per-command cooldown management
- **Environment Configuration**: Secure configuration management with dotenv

## Project Structure

```
Discord-Handler-Js/
├── package.json                  # Project dependencies and scripts
├── src/                          # Source code
│   ├── index.js                  # Main bot entry point
│   ├── config.js                 # Bot configuration
│   ├── Core/                     # Core utilities and webhooks
│   │   ├── commandUtils.js       # Utilities for handling commands
│   │   ├── emojis.js             # Centralized emoji definitions
│   │   ├── errorWebhook.js       # Error reporting via webhook
│   │   ├── joinGuildWebhook.js   # Webhook when the bot joins a guild
│   │   ├── leaveGuildWebhook.js  # Webhook when the bot leaves a guild
│   │   ├── prefixCommandWebhook.js   # Webhook logging for prefix commands
│   │   ├── readyWebhook.js       # Webhook logging for bot ready event
│   │   └── slashCommandWebhook.js    # Webhook logging for slash commands
│   ├── Database/
│   │   └── mongo.js              # MongoDB connection setup
│   ├── Events/                   # Discord event handlers
│   │   ├── error.js              # Global error event handler
│   │   ├── guildCreate.js        # Handler when bot joins a server
│   │   ├── guildDelete.js        # Handler when bot leaves a server
│   │   ├── interactionCreate.js  # Handles slash command interactions
│   │   ├── messageCreate.js      # Handles prefix commands
│   │   └── ready.js              # Bot ready event
│   ├── Handlers/                 # Handlers for modularity
│   │   ├── AntiCrash.js          # Crash prevention and error handling
│   │   ├── Commands.js           # Slash command loader/registration
│   │   ├── Events.js             # Event handler loader
│   │   ├── logger.js             # Logger for bot activity
│   │   ├── Models.js             # Models loader
│   │   └── Prefix.js             # Prefix command loader
│   ├── Models/
│   │   ├── userModel.js          # Mongoose schema for user data
│   │   └── config.js             # Bot configuration model
│   └── Commands/
│       ├── Prefix/               # Prefix commands
│       │   └── Public/ping.js    # Example prefix ping command
│       └── Slash/                # Slash commands
│           └── Public/ping.js    # Example slash ping command
```

## Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/RealMtrx/Discord-Handler-Js.git
   cd Discord-Handler-Js
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Environment Setup**

   Copy `.env.example` to `.env` and fill in your values:

   ```env
   TOKEN=your_bot_token_here
   PREFIX=!
   BOT_NAME=Discord Handler
   MONGO_URI=mongodb://localhost:27017/discord-handler
   ERROR_WEBHOOK=https://discord.com/api/webhooks/your_webhook
   GUILD_LOG_WEBHOOK=https://discord.com/api/webhooks/your_webhook
   ```

   ⚠️ **Security Note**: Never commit your `.env` file to version control!

4. **Run the bot**

   ```bash
   npm start
   ```

## Dependencies

- **discord.js**: ^14.11.0 - Discord API wrapper
- **mongoose**: ^7.5.0 - MongoDB ODM
- **dotenv**: ^17.2.1 - Environment variable management
- **boxen**: ^7.0.0 - Boxed UI for startup report
- **chalk**: ^5.3.0 - Terminal colors

## Command Development

### Creating Slash Commands

Create a new file in `src/Commands/Slash/[category]/[name].js`:

```javascript
import { SlashCommandBuilder } from 'discord.js';

export default {
  data: new SlashCommandBuilder()
    .setName('commandname')
    .setDescription('Command description'),
  async execute(interaction) {
    await interaction.reply('Response');
  }
};
```

### Creating Prefix Commands

Create a new file in `src/Commands/Prefix/[category]/[name].js`:

```javascript
export default {
  name: 'commandname',
  description: 'Command description',
  execute(client, message, args) {
    message.reply('Response');
  }
};
```

---

**Discord Handler** - A modern, scalable Discord bot framework built with JavaScript.

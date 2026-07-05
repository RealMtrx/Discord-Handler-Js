# Discord Handler

A modern, feature-rich Discord bot handler built with **Discord.js v14**, featuring both slash commands and prefix commands with a robust modular architecture designed for scalability and maintainability.

## 🚀 Features

- **Dual Command System**: Support for both slash commands and prefix commands
- **Modular Architecture**: Clean separation of concerns with dedicated handlers
- **Anti-Crash System**: Comprehensive error handling and monitoring
- **Event-Driven**: Fully event-driven architecture
- **ES6 Modules**: Modern JavaScript with ES6 module syntax
- **Environment Configuration**: Secure configuration management with dotenv

## 📁 Project Structure

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
│       │   └── Public/
│       │       └── ping.js       # Example prefix ping command
│       └── Slash/                # Slash commands
│           └── Public/
│               └── ping.js       # Example slash ping command
```

## 🔧 Installation

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

   Open `src/config.js` file and set the following variables:

   ```javascript
   token: "your_bot_token",
   clientId: "your_client_id",
   prefix: "your_prefix",
   ownerIds: ["owner_id_1", "owner_id_2"],
   MONGODB_URI: "your_mongo_uri",
   errorWebhook: "your_error_webhook",
   slashCommandWebhook: "your_slash_webhook",
   prefixCommandWebhook: "your_prefix_webhook",
   joinGuildWebhook: "your_join_webhook",
   leaveGuildWebhook: "your_leave_webhook",
   readyWebhook: "your_ready_webhook",
   ```

   ⚠️ **Security Note**: Never commit your `config.js` file to version control!

4. **Run the bot**

   ```bash
   npm start
   ```

## 📋 Dependencies

- **discord.js**: ^14.11.0 - Discord API wrapper
- **@discordjs/rest**: ^2.5.1 - REST API client
- **discord-api-types**: ^0.38.14 - TypeScript definitions
- **dotenv**: ^16.3.1 - Environment variable management
- **axios**: ^1.10.0 - HTTP client for webhooks
- **node-fetch**: ^3.3.2 - Fetch API for Node.js

## 📝 Command Development

### Creating Slash Commands

Create new slash commands in `src/Commands/Slash/[category]/[command].js`:

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

Create new prefix commands in `src/Commands/Prefix/[category]/[command].js`:

```javascript
export default {
  name: 'commandname',
  description: 'Command description',
  aliases: ['alias1', 'alias2'],
  execute(client, message, args) {
    message.reply('Response');
  }
};
```

---

**Discord Handler** - A modern, scalable Discord bot framework built with JavaScript.

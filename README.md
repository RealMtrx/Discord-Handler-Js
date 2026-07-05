<div align="center">
  <h1>Discord Handler — JavaScript</h1>
  <p><strong>A production-ready Discord bot framework built with Discord.js v14 and MongoDB — slash commands, prefix commands, anti-crash, webhook logging, and a modular <code>src/</code> architecture.</strong></p>

  <p>
    <a href="https://github.com/RealMtrx/Discord-Handler-Js/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
    <a href="https://github.com/RealMtrx/Discord-Handler-Js/releases"><img src="https://img.shields.io/badge/version-0.9.0--beta-yellow" alt="Version 0.9.0 Beta"></a>
    <a href="https://github.com/RealMtrx/Discord-Handler-Js/stargazers"><img src="https://img.shields.io/github/stars/RealMtrx/Discord-Handler-Js" alt="Stars"></a>
    <a href="https://github.com/RealMtrx/Discord-Handler-Js/issues"><img src="https://img.shields.io/github/issues/RealMtrx/Discord-Handler-Js" alt="Issues"></a>
    <a href="https://github.com/RealMtrx/Discord-Handler-Js/network"><img src="https://img.shields.io/github/forks/RealMtrx/Discord-Handler-Js" alt="Forks"></a>
    <a href="https://github.com/RealMtrx/Discord-Handler/graphs/contributors"><img src="https://img.shields.io/badge/ecosystem-26%20repos-brightgreen" alt="26 Repos"></a>
    <a href="https://discord.gg/0hu2"><img src="https://img.shields.io/badge/discord-0hu2-5865F2" alt="Discord"></a>
  </p>

  <br>

  <p>
    <a href="#-features">Features</a> •
    <a href="#-quick-start">Quick Start</a> •
    <a href="#-project-structure">Structure</a> •
    <a href="#-api-reference">API</a> •
    <a href="#-database-edition">SQL Edition</a> •
    <a href="#-related-repositories">Ecosystem</a>
  </p>
</div>

---

## Overview

Discord Handler JavaScript is a modular, production-ready Discord bot framework built on **Discord.js v14** with **MongoDB** storage. It provides a complete foundation for building Discord bots with slash commands, prefix commands, event handling, anti-crash protection, and webhook-based logging — all organized in a clean, scalable `src/` directory structure.

This is the **reference implementation** for the Discord Handler ecosystem. All 12 other language implementations follow the same architecture and patterns.

> **Version:** 0.9.0 (Stable Beta) — Part of the [Discord Handler](https://github.com/RealMtrx/Discord-Handler) ecosystem (26 repos across 13 languages).

---

## Features

- **Dual Command System** — Slash commands and prefix commands with auto-registration
- **MongoDB Integration** — Persistent data storage with Mongoose ODM
- **Modular Architecture** — Clean separation: Commands, Events, Handlers, Core, Database, Models
- **Anti-Crash Protection** — Handles `unhandledRejection`, `uncaughtException`, and `warning` events
- **Webhook Logging** — Dedicated webhooks for errors, slash commands, prefix commands, guild joins/leaves, and bot ready events
- **Cooldown System** — Per-command rate limiting with automatic periodic cleanup
- **Dynamic Command Loading** — Automatically discovers and registers commands from the filesystem
- **Unicode Emoji System** — Flat-export emoji constants for consistent rendering across platforms
- **Environment Configuration** — Secure token and secrets management via `dotenv`
- **Startup Report** — Color-coded terminal banner showing loaded commands, events, and connection status
- **Graceful Shutdown** — Proper cleanup on SIGINT and SIGTERM signals

---

## Quick Start

```bash
# Clone the repository
git clone https://github.com/RealMtrx/Discord-Handler-Js.git
cd Discord-Handler-Js

# Install dependencies
npm install

# Configure environment
cp .env.example .env
# Edit .env with your bot token, client ID, and MongoDB URI

# Start the bot
npm start
```

### Prerequisites

- **Node.js 18+** — Runtime environment
- **MongoDB** — Local or Atlas instance
- **Discord Application** — Bot token and client ID from the [Discord Developer Portal](https://discord.com/developers/applications)

---

## Project Structure

```
Discord-Handler-Js/
├── package.json
├── .env.example
├── src/
│   ├── index.js                 # Entry point — initializes everything
│   ├── config.js                # Configuration loader (env vars)
│   ├── Core/                    # Shared utilities
│   │   ├── commandUtils.js      # Cooldown, error formatting, logging
│   │   ├── emojis.js            # Unicode emoji constants
│   │   ├── errorWebhook.js      # Error reporting webhook
│   │   ├── joinGuildWebhook.js  # Guild join notification webhook
│   │   ├── leaveGuildWebhook.js # Guild leave notification webhook
│   │   ├── prefixCommandWebhook.js
│   │   ├── readyWebhook.js      # Bot ready event webhook
│   │   └── slashCommandWebhook.js
│   ├── Database/
│   │   └── mongo.js             # MongoDB connection with Mongoose
│   ├── Events/                  # Discord event listeners
│   │   ├── error.js
│   │   ├── guildCreate.js
│   │   ├── guildDelete.js
│   │   ├── interactionCreate.js
│   │   ├── messageCreate.js
│   │   └── ready.js
│   ├── Handlers/                # Loaders and registrars
│   │   ├── AntiCrash.js         # Global error handlers
│   │   ├── Commands.js          # Slash command loader and Discord API registration
│   │   ├── Events.js            # Event file loader
│   │   ├── Models.js            # Model file loader
│   │   ├── Prefix.js            # Prefix command loader
│   │   └── logger.js            # Startup report logger
│   ├── Models/
│   │   └── userModel.js         # Mongoose User model
│   └── Commands/
│       ├── Slash/Public/ping.js
│       └── Prefix/Public/ping.js
```

---

## API Reference

### Core Functions

| Function | Location | Description |
| -------- | -------- | ----------- |
| `checkCooldown(userId, commandName, cooldownTime)` | `Core/commandUtils.js` | Checks and sets per-command cooldowns |
| `logCommandUsage(user, commandName, guildName)` | `Core/commandUtils.js` | Logs command usage (placeholder) |
| `formatError(error, commandName)` | `Core/commandUtils.js` | Formats error objects for logging |
| `sendErrorToWebhook(error, context)` | `Core/errorWebhook.js` | Sends error reports to Discord webhook |
| `sendBotReadyEvent(client)` | `Core/readyWebhook.js` | Sends bot online notification |
| `sendGuildJoinEvent(guild, client)` | `Core/joinGuildWebhook.js` | Sends guild join notification |
| `sendGuildLeaveEvent(guild, client)` | `Core/leaveGuildWebhook.js` | Sends guild leave notification |
| `sendSlashCommandUsage(user, commandName, guildName)` | `Core/slashCommandWebhook.js` | Logs slash command usage |
| `sendPrefixCommandUsage(user, commandName, guildName)` | `Core/prefixCommandWebhook.js` | Logs prefix command usage |

### Database

| Function | Location | Description |
| -------- | -------- | ----------- |
| `connectMongo()` | `Database/mongo.js` | Connects to MongoDB via Mongoose |

### Handlers

| Function | Location | Description |
| -------- | -------- | ----------- |
| `loadCommands(client)` | `Handlers/Commands.js` | Scans Commands/Slash, imports, and registers with Discord API |
| `loadPrefix(client)` | `Handlers/Prefix.js` | Scans Commands/Prefix and registers in-memory |
| `loadEvents(client)` | `Handlers/Events.js` | Scans Events directory and attaches listeners |
| `loadModels()` | `Handlers/Models.js` | Scans Models directory and imports each |
| `AntiCrash(client)` | `Handlers/AntiCrash.js` | Attaches global process error handlers |

---

## Adding Commands

### Slash Command

```javascript
// src/Commands/Slash/Public/hello.js
import { SlashCommandBuilder } from 'discord.js';

export default {
  data: new SlashCommandBuilder()
    .setName('hello')
    .setDescription('Say hello!'),
  async execute(interaction) {
    await interaction.reply('Hello! 👋');
  }
};
```

### Prefix Command

```javascript
// src/Commands/Prefix/Public/hello.js
export default {
  name: 'hello',
  description: 'Say hello!',
  async execute(client, message, args) {
    await message.reply('Hello! 👋');
  }
};
```

---

## Database Edition

This is the **MongoDB edition**. A **SQL edition** using Sequelize ORM is also available:

| Feature | MongoDB Edition | SQL Edition |
| ------- | --------------- | ----------- |
| Repository | [Discord-Handler-Js](https://github.com/RealMtrx/Discord-Handler-Js) | [Discord-Handler-Js-Sequelize](https://github.com/RealMtrx/Discord-Handler-Js-Sequelize) |
| Database | MongoDB | SQLite, PostgreSQL, MySQL, MSSQL |
| ORM | Mongoose | Sequelize |
| Dialects | MongoDB only | Multi-dialect via config |

---

## Related Repositories

Discord Handler JavaScript is part of a **26-repo ecosystem**. Here are the other repositories:

### Core Framework (MongoDB)

| Language | Repository |
| -------- | ---------- |
| TypeScript | [Discord-Handler-Ts](https://github.com/RealMtrx/Discord-Handler-Ts) |
| Go | [Discord-Handler-Go](https://github.com/RealMtrx/Discord-Handler-Go) |
| Rust | [Discord-Handler-Rs](https://github.com/RealMtrx/Discord-Handler-Rs) |
| Python | [Discord-Handler-Py](https://github.com/RealMtrx/Discord-Handler-Py) |
| C# | [Discord-Handler-Cs](https://github.com/RealMtrx/Discord-Handler-Cs) |
| Java | [Discord-Handler-Java](https://github.com/RealMtrx/Discord-Handler-Java) |
| Kotlin | [Discord-Handler-Kt](https://github.com/RealMtrx/Discord-Handler-Kt) |
| C++ | [Discord-Handler-Cpp](https://github.com/RealMtrx/Discord-Handler-Cpp) |
| Dart | [Discord-Handler-Dart](https://github.com/RealMtrx/Discord-Handler-Dart) |
| Ruby | [Discord-Handler-Rb](https://github.com/RealMtrx/Discord-Handler-Rb) |
| Lua | [Discord-Handler-Lua](https://github.com/RealMtrx/Discord-Handler-Lua) |
| PHP | [Discord-Handler-Php](https://github.com/RealMtrx/Discord-Handler-Php) |

### Database Editions (SQL)

| Language | Repository |
| -------- | ---------- |
| JavaScript | [Discord-Handler-Js-Sequelize](https://github.com/RealMtrx/Discord-Handler-Js-Sequelize) |
| TypeScript | [Discord-Handler-Ts-Sequelize](https://github.com/RealMtrx/Discord-Handler-Ts-Sequelize) |
| Go | [Discord-Handler-Go-Sequelize](https://github.com/RealMtrx/Discord-Handler-Go-Sequelize) |
| Rust | [Discord-Handler-Rs-Sequelize](https://github.com/RealMtrx/Discord-Handler-Rs-Sequelize) |
| Python | [Discord-Handler-Py-Sequelize](https://github.com/RealMtrx/Discord-Handler-Py-Sequelize) |
| C# | [Discord-Handler-Cs-Sequelize](https://github.com/RealMtrx/Discord-Handler-Cs-Sequelize) |
| Java | [Discord-Handler-Java-Sequelize](https://github.com/RealMtrx/Discord-Handler-Java-Sequelize) |
| Kotlin | [Discord-Handler-Kt-Sequelize](https://github.com/RealMtrx/Discord-Handler-Kt-Sequelize) |
| C++ | [Discord-Handler-Cpp-Sequelize](https://github.com/RealMtrx/Discord-Handler-Cpp-Sequelize) |
| Dart | [Discord-Handler-Dart-Sequelize](https://github.com/RealMtrx/Discord-Handler-Dart-Sequelize) |
| Ruby | [Discord-Handler-Rb-Sequelize](https://github.com/RealMtrx/Discord-Handler-Rb-Sequelize) |
| Lua | [Discord-Handler-Lua-Sequelize](https://github.com/RealMtrx/Discord-Handler-Lua-Sequelize) |
| PHP | [Discord-Handler-Php-Sequelize](https://github.com/RealMtrx/Discord-Handler-Php-Sequelize) |

### Hub

| Repository | Description |
| ---------- | ----------- |
| [Discord-Handler](https://github.com/RealMtrx/Discord-Handler) | Central hub — documentation, examples, changelog, roadmap |

---

## License

MIT License — Copyright © 2026 Mtrx

---

<div align="center">
  <sub>Built by <strong>Mtrx</strong> — Discord: <strong>0hu2</strong></sub>
  <br>
  <sub><a href="https://github.com/RealMtrx/Discord-Handler">Discord Handler Ecosystem</a></sub>
</div>

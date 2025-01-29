# Aisyah AI Telegraph

A Cloudflare Worker service that powers the Telegram bot interface for the Aisyah AI ecosystem, providing natural language interaction, voice message processing, and settings management capabilities.

## Overview

This service acts as the main communication interface between users and the Aisyah AI ecosystem through Telegram. It handles various types of interactions including text messages, voice messages, and settings management, while integrating with other services in the ecosystem for specialized tasks.

## Features

- Natural language conversation through Telegram
- Voice message transcription and processing
- Settings management through inline keyboards
- Rate limiting and concurrency control
- Chat history management
- Multi-user support
- Private and group chat capabilities
- Command handling
- Webhook integration
- Redis-based state management

## Commands

- `/start` - Initialize conversation with the bot
- `/description` - Get information about the bot
- `/forget` - Clear chat history
- `/help` - Get help about bot capabilities
- `/privacy` - Get information about data privacy
- `/settings` - Manage bot settings

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Telegraph Worker"
}
```

### POST /webhooks/telegram/setup

Sets up the Telegram webhook for the bot.

### POST /webhooks/telegram

Handles incoming Telegram updates.

### POST /webhooks/reminders-api

Handles incoming reminder notifications.

### GET /settings/:key

Retrieves settings for a specific chat.

### POST /settings/:key

Updates settings for a specific chat.

### DELETE /settings/:key

Deletes settings for a specific chat.

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in the required environment variables:
```
TELEGRAM_BOT_TOKEN=your-bot-token-here
TELEGRAM_BOT_INFO=your-bot-info-here
UPSTASH_REDIS_REST_URL=your-redis-url-here
UPSTASH_REDIS_REST_TOKEN=your-redis-token-here
```

2. Copy `wrangler.toml.example` to `wrangler.toml` and adjust the configuration as needed.

3. Install dependencies:
```bash
npm install
```

## Development

To run the worker locally:
```bash
npm run dev
```

To deploy to Cloudflare:
```bash
npm run deploy
```

## Environment Variables

- `TELEGRAM_BOT_TOKEN`: Your Telegram bot token (required)
- `TELEGRAM_BOT_INFO`: JSON string containing bot information (required)
- `TELEGRAM_API_BASE_URL`: Telegram API base URL
- `UPSTASH_REDIS_REST_URL`: Upstash Redis REST URL (required)
- `UPSTASH_REDIS_REST_TOKEN`: Upstash Redis REST token (required)
- `CHAT_HISTORY_LIMIT`: Maximum number of messages to keep in chat history
- `CLOUDFLARE_SUBDOMAIN`: Cloudflare subdomain for service URLs

## Dependencies

- `@packages/shared`: Shared types and utilities
- `grammy`: Telegram Bot API framework
- `hono`: Web framework
- Other Aisyah AI services:
  - `aisyah-ai-agent`: Natural language processing
  - `aisyah-ai-whisper`: Voice transcription
  - `aisyah-ai-sonata`: Audio processing

## Features in Detail

### Message Handling
- Text message processing
- Voice message transcription
- Photo and file handling
- Group chat interactions
- Message mention detection
- Reply detection

### Settings Management
- Chat history limit configuration
- Rate limiting settings
- Inline keyboard interface
- Settings persistence

### State Management
- Redis-based chat history
- Rate limiting
- Concurrency control
- Recent interactions tracking

### Error Handling
- Rate limit enforcement
- Concurrent request handling
- API error handling
- Invalid input validation

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- Telegram API interactions
- Environment configurations
- Settings management
- Message handling
- State management 
# 🌟 Aisyah AI 🌟

![Avatar](https://github.com/husniadil/aisyah-ai/blob/main/assets/avatar.jpg?raw=true)

Aisyah AI is a powerful Telegram bot built with Cloudflare Workers that combines multiple AI capabilities. It can browse the web, set reminders, speak, predict weather, analyze images, and understand voice messages. The bot maintains context in conversations through Redis, making it perfect for both private chats and group interactions.

## 📸 Screenshots & Demo

[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/chat.png?raw=true" width="200" alt="chat" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/chat.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/group-chat.png?raw=true" width="200" alt="group-chat" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/group-chat.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-llm-model.png?raw=true" width="200" alt="settings-llm-model" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-llm-model.png)
[<img src="https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-persona.png?raw=true" width="200" alt="settings-persona" />](https://github.com/husniadil/aisyah-ai/blob/main/assets/settings-persona.png)

## ✨ Features

- **🤖 Advanced AI Capabilities**
  - Natural language understanding with GPT models
  - Image analysis and object recognition
  - Speech-to-text and text-to-speech conversion
  - Context-aware conversations in both private and group chats

- **🎯 Smart Tools**
  - Web browsing and information retrieval
  - Real-time weather forecasts
  - Task reminders and notifications
  - Group chat support with context retention

- **☁️ Modern Architecture**
  - Built on Cloudflare Workers for high scalability
  - Microservices architecture for modularity
  - Redis-powered chat history
  - Cost-effective serverless deployment

- **🔗 API Integrations**
  - OpenAI GPT for language processing
  - Google Custom Search for web browsing
  - OpenWeatherMap for weather data
  - Telegram Bot API for messaging
  - Supabase for file storage
  - Additional services for enhanced capabilities

### 🤔 Why OpenAI Only?

We've chosen to exclusively support OpenAI models (particularly gpt-3.5-turbo and gpt-4o-mini) for several reasons:

1. **Model Consistency**: OpenAI models provide the most consistent and high-quality responses across different languages and use cases.
2. **Cost-Effectiveness**: gpt-4o-mini offers an excellent balance between output quality and pricing.
3. **Multilingual Capability**: After extensive testing, OpenAI models demonstrated superior performance in handling multiple languages naturally.
4. **Implementation Simplicity**: While services like OpenRouter offer access to various models, supporting them would introduce additional complexity in model name mappings and response handling.

Note: We understand the interest in alternative models and providers (like OpenRouter, Anthropic, etc.). However, to maintain code simplicity and ensure consistent bot behavior, we've decided to focus on OpenAI's offerings. If you need to use different models, you'll need to fork the project and modify the model configurations accordingly.

## 📝 Usage

### Basic Commands
- `/start` - Begin interaction with the bot
- `/settings` - Configure bot settings (LLM model, persona, voice, etc.)
- `/help` - Get help about available commands

**Note**: This is a personal project designed for learning and experimentation purposes.

## 🏗️ Project Structure

The project is organized into several microservices:

- `aisyah-ai-telegraph`: Main orchestrator that handles Telegram interactions
- `aisyah-ai-agent`: Core AI agent that processes requests
- `aisyah-ai-explorer`: Web browsing capability
- `aisyah-ai-reminder`: Reminder management
- `aisyah-ai-sonata`: Text-to-speech service
- `aisyah-ai-storm`: Weather prediction
- `aisyah-ai-vision`: Image analysis
- `aisyah-ai-whisper`: Speech-to-text service

## 🚀 Quick Start

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS version recommended)
- [Yarn](https://yarnpkg.com/) (v4.3.1 or later)
- [Cloudflare Account](https://dash.cloudflare.com/sign-up) (Free tier works)
- [Telegram Bot Token](https://core.telegram.org/bots#how-do-i-create-a-bot)
- [OpenAI API Key](https://platform.openai.com/api-keys)
- Redis instance for chat history (You can use [Upstash](https://upstash.com/) free tier)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/husniadil/aisyah-ai.git
   cd aisyah-ai
   ```

2. Install dependencies:
   ```bash
   yarn install
   ```

3. Set up Cloudflare:
   First, get your Cloudflare API Token:
   1. Go to https://dash.cloudflare.com/profile/api-tokens
   2. Locate "Edit Cloudflare Workers", then "Use Template"
   3. Fill out the rules
   4. Click "Continue to summary" and create the token
   5. Export the token as an environment variable:
      ```bash
      export CLOUDFLARE_API_TOKEN=your_api_token_here
      ```
   6. For persistent configuration, add it to your shell profile (~/.zshrc, ~/.bashrc, etc.):
      ```bash
      echo 'export CLOUDFLARE_API_TOKEN=your_api_token_here' >> ~/.zshrc
      ```

   Note: Do not use `wrangler login` as it conflicts with the API token authentication method.

4. Configure environment files:
   ```bash
   # Copy Cloudflare configuration files
   cp packages/aisyah-ai-agent/wrangler.toml.example packages/aisyah-ai-agent/wrangler.toml
   cp packages/aisyah-ai-explorer/wrangler.toml.example packages/aisyah-ai-explorer/wrangler.toml
   cp packages/aisyah-ai-reminder/wrangler.toml.example packages/aisyah-ai-reminder/wrangler.toml
   cp packages/aisyah-ai-sonata/wrangler.toml.example packages/aisyah-ai-sonata/wrangler.toml
   cp packages/aisyah-ai-storm/wrangler.toml.example packages/aisyah-ai-storm/wrangler.toml
   cp packages/aisyah-ai-telegraph/wrangler.toml.example packages/aisyah-ai-telegraph/wrangler.toml
   cp packages/aisyah-ai-vision/wrangler.toml.example packages/aisyah-ai-vision/wrangler.toml
   cp packages/aisyah-ai-whisper/wrangler.toml.example packages/aisyah-ai-whisper/wrangler.toml

   # Copy environment variables
   cp packages/aisyah-ai-agent/.dev.vars.example packages/aisyah-ai-agent/.dev.vars
   cp packages/aisyah-ai-explorer/.dev.vars.example packages/aisyah-ai-explorer/.dev.vars
   cp packages/aisyah-ai-reminder/.dev.vars.example packages/aisyah-ai-reminder/.dev.vars
   cp packages/aisyah-ai-sonata/.dev.vars.example packages/aisyah-ai-sonata/.dev.vars
   cp packages/aisyah-ai-storm/.dev.vars.example packages/aisyah-ai-storm/.dev.vars
   cp packages/aisyah-ai-telegraph/.dev.vars.example packages/aisyah-ai-telegraph/.dev.vars
   cp packages/aisyah-ai-vision/.dev.vars.example packages/aisyah-ai-vision/.dev.vars
   cp packages/aisyah-ai-whisper/.dev.vars.example packages/aisyah-ai-whisper/.dev.vars
   ```

5. Configure package-specific settings:

   ### Cloudflare KV Namespaces
   Create the required KV namespaces and make note of their IDs:
   ```bash
   # For settings storage
   yarn w aisyah-ai-agent wrangler kv:namespace create SETTINGS
   
   # For chat history
   yarn w aisyah-ai-telegraph wrangler kv:namespace create CHAT_HISTORY
   
   # For reminders
   yarn w aisyah-ai-reminder wrangler kv:namespace create REMINDERS
   ```

   ### Package-specific Configurations

   #### aisyah-ai-telegraph (Main Bot)
   ```bash
   # In packages/aisyah-ai-telegraph/.dev.vars
   CLOUDFLARE_SUBDOMAIN=your_subdomain
   TELEGRAM_BOT_TOKEN=your_telegram_bot_token
   UPSTASH_REDIS_REST_URL=your_redis_rest_url
   UPSTASH_REDIS_REST_TOKEN=your_redis_rest_token
   ```

   #### aisyah-ai-agent (Core AI)
   ```bash
   # In packages/aisyah-ai-agent/.dev.vars
   OPENAI_API_KEY=your_openai_api_key
   LANGCHAIN_API_KEY=your_langchain_api_key
   CLOUDFLARE_SUBDOMAIN=your_subdomain
   AGENT_PERSONA_AISYAH_DEFAULT=your_system_prompt_for_persona_default
   AGENT_PERSONA_AISYAH_JAWIR=your_system_prompt_for_persona_jawir
   AGENT_PERSONA_PERSONAL_ASSISTANT=your_system_prompt_for_persona_personal_assistant
   ```

   #### aisyah-ai-vision (Image Analysis)
   ```bash
   # In packages/aisyah-ai-vision/.dev.vars
   OPENAI_API_KEY=your_openai_api_key
   ```

   #### aisyah-ai-whisper (Speech-to-Text)
   ```bash
   # In packages/aisyah-ai-whisper/.dev.vars
   OPENAI_API_KEY=your_openai_api_key
   ```

   #### aisyah-ai-sonata (Text-to-Speech)
   ```bash
   # In packages/aisyah-ai-sonata/.dev.vars
   OPENAI_API_KEY=your_openai_api_key
   # Get from https://supabase.io
   SUPABASE_URL=your_supabase_project_url
   SUPABASE_KEY=your_supabase_storage_key
   # Get from https://elevenlabs.io
   ELEVENLABS_API_KEY=your_elevenlabs_api_key
   ```

   #### aisyah-ai-storm (Weather)
   ```bash
   # In packages/aisyah-ai-storm/.dev.vars
   OPEN_WEATHER_MAP_API_KEY=your_openweathermap_api_key
   ```

   #### aisyah-ai-explorer (Web Browser)
   ```bash
   # In packages/aisyah-ai-explorer/.dev.vars
   # Get from https://programmablesearchengine.google.com/
   GOOGLE_SEARCH_API_KEY=your_google_api_key
   GOOGLE_SEARCH_ENGINE_ID=your_search_engine_id
   ```

   #### aisyah-ai-reminder (Reminders)
   ```bash
    # In packages/aisyah-ai-reminder/.dev.vars
    REMINDERS_APP_ID=your_reminders_app_id
    REMINDERS_API_KEY=your_reminders_api_key
    ```

   ### Update wrangler.toml Files
   Update each package's `wrangler.toml` with the corresponding KV namespace IDs from the previous step:

   ```toml
   # In packages/aisyah-ai-telegraph/wrangler.toml
   kv_namespaces = [
     { binding = "CHAT_HISTORY", id = "your_chat_history_namespace_id" }
   ]

   # In packages/aisyah-ai-agent/wrangler.toml
   kv_namespaces = [
     { binding = "SETTINGS", id = "your_settings_namespace_id" }
   ]

   # In packages/aisyah-ai-reminder/wrangler.toml
   kv_namespaces = [
     { binding = "REMINDERS", id = "your_reminders_namespace_id" }
   ]
   ```

6. Deploy the workers:
   ```bash
   yarn deploy
   ```

7. Set up your Telegram bot:
   - Create a new bot with [@BotFather](https://t.me/botfather)
   - Set the webhook URL to your Cloudflare Worker endpoint
   - Configure the bot settings through Telegram chat interface

## 🛠️ Development

### Available Scripts

- `yarn w`: Run workspace-specific commands
- `yarn deploy`: Deploy all workers
- `yarn types`: Generate TypeScript types
- `yarn format`: Format code using Biome

### Adding New Features

1. Create a new package in the `packages` directory
2. Implement your feature using Cloudflare Workers
3. Add configuration in `wrangler.toml`
4. Register the new capability in `aisyah-ai-agent`

## 🔧 Additional Setup

### Redis Configuration

1. Set up a Redis instance:
   - Create a free Redis database at [Upstash](https://upstash.com/)
   - Get your Redis connection URL and authentication details

2. Configure Redis in your environment:
   ```bash
   # Add to packages/aisyah-ai-telegraph/.dev.vars
   UPSTASH_REDIS_REST_URL=your_redis_rest_url
   UPSTASH_REDIS_REST_TOKEN=your_redis_rest_token
   ```

### Required API Keys

Make sure to obtain and configure these API keys:
- OpenAI API key for LLM and vision capabilities
- LangChain API key for enhanced language processing
- OpenWeatherMap API key for weather forecasts
- Supabase project and storage keys for file handling

Add them to the respective `.dev.vars` files in each package.

## ❗ Troubleshooting

### Common Issues

1. **Worker Deployment Fails**
   - Ensure Cloudflare API token has correct permissions
   - Check if worker names in `wrangler.toml` are unique
   - Verify KV namespace bindings are correct

2. **Bot Not Responding**
   - Confirm webhook URL is correctly set
   - Check Telegram bot token validity
   - Verify Redis connection is working

3. **Features Not Working**
   - Ensure all required API keys are valid and properly configured
   - Check corresponding worker logs in Cloudflare dashboard
   - Verify environment variables are set correctly

### Debug Mode

Enable debug mode by setting:
```bash
# Add to .dev.vars
DEBUG_MODE=true
```

This will provide more detailed logs in the worker console.

### Getting Help

If you encounter issues:
1. Check the [Issues](https://github.com/husniadil/aisyah-ai/issues) page
2. Review Cloudflare Workers logs
3. Enable debug mode for more detailed logging

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

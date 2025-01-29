# Aisyah AI Agent

A Cloudflare Worker service that provides an intelligent conversational agent powered by OpenAI's GPT models and LangChain, with access to multiple tools and capabilities.

## Overview

This service is the core intelligence of the Aisyah AI ecosystem, handling natural language understanding and generation. It integrates with multiple tools and services to provide a comprehensive conversational experience with various capabilities.

## Features

- Advanced language understanding and generation using OpenAI's GPT models
- Multiple persona support (Default Aisyah, Jawir Aisyah, Personal Assistant)
- Tool integration for extended capabilities:
  - Calculator for mathematical operations
  - Wikipedia for knowledge queries
  - Vision for image analysis
  - Sonata for text-to-speech
  - Whisper for speech-to-text
  - Reminder for scheduling
  - Storm for weather information
  - Explorer for web searches
- Chat history management
- Streaming response support
- Configurable LLM settings
- Built with TypeScript, LangChain, and Hono framework

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Agent Worker"
}
```

### POST /chat

Processes a chat message and returns a response.

**Request Body:**
```typescript
{
  chatId: string;        // Unique identifier for the chat
  messageId: string;     // Unique identifier for the message
  senderId: string;      // Identifier of the message sender
  senderName: string;    // Name of the message sender
  message: string;       // The chat message content
  chatHistory: Array<{   // Previous messages in the conversation
    type: "human" | "ai";
    message: string;
    senderName: string;
    timestamp: string;
  }>;
}
```

**Response:**
```typescript
{
  data: string;  // The agent's response message
}
```

### POST /chat/stream

Same as `/chat` but returns the response as a stream of text chunks.

### GET /settings/:key

Retrieves agent settings for a specific chat.

### POST /settings/:key

Updates agent settings for a specific chat.

**Request Body:**
```typescript
{
  llm?: {
    model?: string;           // LLM model to use
    maxTokens?: number;       // Maximum tokens in response
    temperature?: number;     // Response randomness (0-1)
    topP?: number;           // Nucleus sampling parameter
    frequencyPenalty?: number;  // Repetition penalty
    presencePenalty?: number;   // Topic diversity penalty
  };
  persona?: "aisyah-default" | "aisyah-jawir" | "personal-assistant";
}
```

### DELETE /settings/:key

Deletes agent settings for a specific chat.

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in the required environment variables:
```
OPENAI_API_KEY=your-openai-api-key-here
AGENT_PERSONA_AISYAH_DEFAULT=your-default-persona-prompt
AGENT_PERSONA_AISYAH_JAWIR=your-jawir-persona-prompt
AGENT_PERSONA_PERSONAL_ASSISTANT=your-assistant-persona-prompt
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

- `OPENAI_API_KEY`: Your OpenAI API key (required)
- `AGENT_LLM_MODEL`: Default LLM model to use
- `AGENT_LLM_MAX_TOKENS`: Default maximum tokens in response
- `AGENT_LLM_TEMPERATURE`: Default temperature setting
- `AGENT_LLM_TOP_P`: Default top_p setting
- `AGENT_LLM_FREQUENCY_PENALTY`: Default frequency penalty
- `AGENT_LLM_PRESENCE_PENALTY`: Default presence penalty
- `AGENT_PERSONA_*`: Persona prompts
- `CLOUDFLARE_SUBDOMAIN`: Subdomain for service URLs

## Dependencies

- `@packages/shared`: Shared types and utilities
- `langchain`: LangChain framework
- `@langchain/openai`: OpenAI integration
- `hono`: Web framework

## Agent Capabilities

The agent provides several core capabilities:
- Natural language understanding and generation
- Context-aware conversations with chat history
- Multiple persona support for different interaction styles
- Tool integration for extended functionality
- Streaming responses for real-time interaction
- Configurable LLM parameters for response tuning

## Personas

The agent supports three distinct personas:
1. **Aisyah Default**: Standard personality
2. **Aisyah Jawir**: Casual, colloquial personality
3. **Personal Assistant**: Professional, task-focused personality

## Error Handling

The service includes comprehensive error handling for:
- Invalid input validation
- LLM API errors
- Tool execution failures
- Settings management errors
- Network failures

All errors are properly logged and return appropriate HTTP status codes with descriptive messages.

## Best Practices

When using this service, consider the following:
- Keep chat history concise to avoid token limits
- Use appropriate personas for different use cases
- Configure LLM parameters based on needs
- Handle streaming responses appropriately
- Implement proper error handling
- Consider rate limits and token usage

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- API request/response structures
- Environment configurations
- LLM settings
- Tool interfaces
- Chat history
- Error handling 
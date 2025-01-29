# Aisyah AI Sonata

A Cloudflare Worker service that provides text-to-speech capabilities using ElevenLabs' voice synthesis technology and Supabase for audio storage.

## Overview

This service is part of the Aisyah AI ecosystem, specifically handling text-to-speech conversion. It uses ElevenLabs for high-quality voice synthesis and stores the generated audio files in Supabase storage, making them accessible via signed URLs.

## Features

- Text-to-speech conversion
- Multiple voice model support
- Configurable voice settings
- Audio file caching in Supabase
- Signed URL generation for secure audio access
- RESTful API endpoints
- Error handling and logging
- Built with TypeScript and Hono framework

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Sonata Worker"
}
```

### POST /speak

Converts text to speech and returns a URL to the generated audio file.

**Request Body:**
```typescript
{
  text: string;      // Text to convert to speech
  metadata: {
    chatId: string;  // Unique identifier for the chat
    messageId: string;  // Unique identifier for the message
  }
}
```

**Response:**
```typescript
{
  data: string;  // Signed URL to the generated audio file
}
```

### GET /settings/:key

Retrieves voice settings for a specific chat.

### POST /settings/:key

Updates voice settings for a specific chat.

**Request Body:**
```typescript
{
  voice: string;  // Voice model name to use
}
```

### DELETE /settings/:key

Deletes voice settings for a specific chat.

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in the required environment variables:
```
ELEVENLABS_API_KEY=your-elevenlabs-api-key-here
SUPABASE_URL=your-supabase-url-here
SUPABASE_KEY=your-supabase-key-here
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

- `ELEVENLABS_API_KEY`: Your ElevenLabs API key (required)
- `ELEVENLABS_VOICE_MODEL_ID`: ElevenLabs voice model ID (required)
- `ELEVENLABS_VOICE_NAME`: Default voice name to use (required)
- `SUPABASE_URL`: Your Supabase project URL (required)
- `SUPABASE_KEY`: Your Supabase API key (required)
- `SUPABASE_STORAGE_KEY`: Supabase storage bucket name (required)

## Dependencies

- `@packages/shared`: Shared types and utilities
- `hono`: Web framework
- `elevenlabs`: ElevenLabs API client
- `@supabase/supabase-js`: Supabase client

## Audio Storage

The service uses Supabase Storage for caching generated audio files:
- Audio files are stored in a structured path: `audio/{chatId}/{messageId}.mp3`
- Files are accessible via signed URLs that expire after 60 seconds
- Existing audio files are reused to minimize API calls to ElevenLabs

## Voice Settings

Voice settings can be configured per chat:
- Custom voice model selection
- Settings are persisted in KV storage
- Fallback to default voice when no custom settings are present

## Error Handling

The service includes comprehensive error handling for:
- Text-to-speech generation failures
- Storage upload/download issues
- Invalid input validation
- Settings management errors
- Network failures

All errors are properly logged and return appropriate HTTP status codes with descriptive messages.

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- API request/response structures
- Environment configurations
- Voice settings
- Storage interactions
- Error handling 
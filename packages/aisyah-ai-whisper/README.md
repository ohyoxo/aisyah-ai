# Aisyah AI Whisper

A Cloudflare Worker service that provides speech-to-text transcription capabilities using OpenAI's Whisper model.

## Overview

This service is part of the Aisyah AI ecosystem, specifically handling audio transcription tasks. It uses OpenAI's Whisper model to convert spoken language in audio files into written text.

## Features

- Audio transcription using OpenAI's Whisper model
- Support for audio file transcription via URL
- RESTful API endpoints
- Error handling and logging
- Built with TypeScript and Hono framework

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Whisper Worker"
}
```

### POST /listen

Transcribes audio from a given URL.

**Request Body:**
```typescript
{
  audioUrl: string;  // URL of the audio file to transcribe
}
```

**Response:**
```typescript
{
  data: string;  // The transcribed text
}
```

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in your OpenAI API key:
```
OPENAI_API_KEY=your-api-key-here
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

## Dependencies

- `@packages/shared`: Shared types and utilities
- `hono`: Web framework
- `openai`: OpenAI API client

## Error Handling

The service includes comprehensive error handling for:
- Invalid input validation
- Audio file fetch failures
- OpenAI API errors
- General runtime errors

All errors are properly logged and return appropriate HTTP status codes.

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. 
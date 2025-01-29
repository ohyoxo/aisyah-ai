# Aisyah AI Vision

A Cloudflare Worker service that provides image analysis and description capabilities using OpenAI's GPT-4 Vision model.

## Overview

This service is part of the Aisyah AI ecosystem, specifically handling image analysis tasks. It uses OpenAI's GPT-4 Vision model to generate natural language descriptions of images provided via URLs.

## Features

- Image analysis and description generation
- Support for image processing via URL
- RESTful API endpoints
- Error handling and logging
- Built with TypeScript and Hono framework
- Uses OpenAI's GPT-4 Vision model for accurate image understanding

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Vision Worker"
}
```

### POST /describe

Generates a natural language description of an image from a given URL.

**Request Body:**
```typescript
{
  imageUrl: string;  // URL of the image to analyze
}
```

**Response:**
```typescript
{
  data: string;  // Natural language description of the image
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
- Image URL fetch failures
- OpenAI API errors
- Description generation failures
- General runtime errors

All errors are properly logged and return appropriate HTTP status codes.

## Image Requirements

- The image must be accessible via a public URL
- Supported formats include JPEG, PNG, WebP, and non-animated GIF
- Maximum image size should comply with OpenAI's API limitations

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- API request/response structures
- Environment configurations
- OpenAI API interactions 
# Aisyah AI Explorer

A Cloudflare Worker service that provides web exploration capabilities, including Google search, image search, and web content extraction.

## Overview

This service is part of the Aisyah AI ecosystem, specifically handling web exploration tasks. It integrates with Google Custom Search API for search capabilities and uses Jina Reader Proxy for web content extraction.

## Features

- Google web search integration
- Google image search with file type filtering
- Web content extraction
- RESTful API endpoints
- Error handling and logging
- Built with TypeScript and Hono framework

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Explorer Worker"
}
```

### POST /search-google

Performs a Google web search with the specified query.

**Request Body:**
```typescript
{
  query: string;  // Search query string
}
```

**Response:**
```typescript
{
  items: Array<{
    title: string;       // Search result title
    link: string;        // URL of the result
    snippet: string;     // Text snippet from the result
    pagemap?: {         // Additional metadata if available
      metatags: Array<Record<string, string>>;
      // Other pagemap properties...
    };
  }>;
}
```

### POST /search-google-images

Performs a Google image search with the specified query and optional file type filter.

**Request Body:**
```typescript
{
  query: string;           // Search query string
  fileType?: ".jpg" | ".png" | ".gif";  // Optional file type filter
}
```

**Response:**
```typescript
{
  items: Array<{
    title: string;       // Image title
    link: string;        // URL of the image
    snippet: string;     // Description of the image
    pagemap?: {
      // Image metadata
    };
  }>;
}
```

### POST /get-web-content

Extracts content from a specified URL using Jina Reader Proxy.

**Request Body:**
```typescript
{
  url: string;  // URL to extract content from
}
```

**Response:**
```typescript
{
  content: string;  // Extracted text content from the webpage
}
```

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in the required environment variables:
```
GOOGLE_SEARCH_API_KEY=your-google-api-key-here
GOOGLE_SEARCH_ENGINE_ID=your-search-engine-id-here
JINA_READER_PROXY_BASE_URL=your-jina-reader-url-here
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

- `GOOGLE_SEARCH_API_KEY`: Your Google Custom Search API key (required)
- `GOOGLE_SEARCH_ENGINE_ID`: Your Google Custom Search Engine ID (required)
- `GOOGLE_SEARCH_API_BASE_URL`: Google Custom Search API base URL
- `JINA_READER_PROXY_BASE_URL`: Jina Reader Proxy base URL (required)

## Dependencies

- `@packages/shared`: Shared types and utilities
- `hono`: Web framework

## Search Features

The service provides several search capabilities:
- Web search with rich metadata
- Image search with file type filtering
- Content extraction from web pages
- Automatic error handling and retries
- Rate limiting compliance

## Error Handling

The service includes comprehensive error handling for:
- Invalid search queries
- API communication failures
- Content extraction failures
- Rate limit exceeded errors
- Network failures

All errors are properly logged and return appropriate HTTP status codes with descriptive messages.

## Best Practices

When using this service, consider the following:
- Keep search queries concise and specific
- Handle rate limits appropriately in your client application
- Cache search results when possible
- Use appropriate file type filters for image searches
- Handle potential errors in your client application
- Consider content extraction limitations for complex web pages

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- API request/response structures
- Environment configurations
- Search result models
- Error handling 
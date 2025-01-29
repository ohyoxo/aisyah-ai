# Aisyah AI Reminder

A Cloudflare Worker service that manages reminders by integrating with an external reminders API, allowing users to schedule and manage notifications.

## Overview

This service is part of the Aisyah AI ecosystem, specifically handling reminder creation and management. It provides a clean interface to schedule reminders with timezone support and custom notification messages.

## Features

- Reminder creation with timezone support
- Custom notification messages
- Date and time scheduling
- RESTful API endpoints
- Error handling and logging
- Built with TypeScript and Hono framework

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Reminder Worker!"
}
```

### POST /remind

Creates a new reminder with the specified details.

**Request Body:**
```typescript
{
  chatId: string;        // Unique identifier for the chat/user
  reminderPrompt: string;  // Message to be sent when reminder triggers
  date: string;          // Date in YYYY-MM-DD format
  time: string;          // Time in HH:mm format
  timeZone: string;      // Timezone identifier (e.g., "Asia/Jakarta")
}
```

**Response:**
```typescript
{
  data: {
    id: number;          // Reminder ID
    title: string;       // Chat ID used as title
    notes: string;       // Reminder message
    date_tz: string;     // Scheduled date
    time_tz: string;     // Scheduled time
    timezone: string;    // Timezone
    created_at: string;  // Creation timestamp
    updated_at: string;  // Last update timestamp
  }
}
```

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in the required environment variables:
```
REMINDERS_API_KEY=your-reminders-api-key-here
REMINDERS_BASE_URL=your-reminders-base-url-here
REMINDERS_APP_ID=your-reminders-app-id-here
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

- `REMINDERS_API_KEY`: Your Reminders API key (required)
- `REMINDERS_BASE_URL`: Base URL for the Reminders API (required)
- `REMINDERS_APP_ID`: Application ID for the Reminders API (required)

## Dependencies

- `@packages/shared`: Shared types and utilities
- `hono`: Web framework

## Reminder Management

The service handles reminder creation with the following features:
- Timezone-aware scheduling
- Custom notification messages
- Unique identification via chat ID
- Automatic date and time conversion

## Error Handling

The service includes comprehensive error handling for:
- Invalid reminder creation requests
- API communication failures
- Invalid date/time formats
- Timezone validation
- Network failures

All errors are properly logged and return appropriate HTTP status codes with descriptive messages.

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- API request/response structures
- Environment configurations
- Reminder data models
- Error handling

## Best Practices

When using this service, consider the following:
- Always provide valid timezone identifiers (e.g., "Asia/Jakarta", "America/New_York")
- Use ISO format for dates (YYYY-MM-DD)
- Use 24-hour format for times (HH:mm)
- Keep reminder messages concise and clear
- Handle potential errors in your client application 
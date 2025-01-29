# Aisyah AI Storm

A Cloudflare Worker service that provides weather information and forecasting capabilities using the OpenWeatherMap API.

## Overview

This service is part of the Aisyah AI ecosystem, specifically handling weather-related queries. It integrates with OpenWeatherMap to provide current weather data and forecasts for cities worldwide.

## Features

- Current weather data retrieval
- Support for multiple units (metric/imperial)
- City-based weather lookup
- RESTful API endpoints
- Error handling and logging
- Built with TypeScript and Hono framework

## API Endpoints

### GET /

Health check endpoint that returns a simple message indicating the worker is running.

**Response:**
```json
{
  "message": "Hi, I'm Storm Worker"
}
```

### POST /predict

Retrieves current weather data for a specified city.

**Request Body:**
```typescript
{
  city: string;    // Name of the city
  unit: string;    // Unit system ('metric' or 'imperial')
}
```

**Response:**
```typescript
{
  coord: {
    lon: number;   // Longitude
    lat: number;   // Latitude
  };
  weather: Array<{
    id: number;    // Weather condition id
    main: string;  // Group of weather parameters (Rain, Snow, etc.)
    description: string;  // Weather condition within the group
    icon: string;  // Weather icon id
  }>;
  base: string;
  main: {
    temp: number;      // Temperature
    feels_like: number;  // Human perception of weather
    temp_min: number;    // Minimum temperature
    temp_max: number;    // Maximum temperature
    pressure: number;    // Atmospheric pressure
    humidity: number;    // Humidity percentage
  };
  visibility: number;
  wind: {
    speed: number;    // Wind speed
    deg: number;      // Wind direction in degrees
  };
  clouds: {
    all: number;      // Cloudiness percentage
  };
  dt: number;         // Time of data calculation
  sys: {
    type: number;
    id: number;
    country: string;  // Country code
    sunrise: number;  // Sunrise time, unix UTC
    sunset: number;   // Sunset time, unix UTC
  };
  timezone: number;   // Shift in seconds from UTC
  id: number;         // City ID
  name: string;       // City name
  cod: number;        // Internal parameter
}
```

## Setup

1. Copy `.dev.vars.example` to `.dev.vars` and fill in your OpenWeatherMap API key:
```
OPEN_WEATHER_MAP_API_KEY=your-api-key-here
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

- `OPEN_WEATHER_MAP_API_KEY`: Your OpenWeatherMap API key (required)
- `OPEN_WEATHER_MAP_BASE_URL`: OpenWeatherMap API base URL (defaults to 'https://api.openweathermap.org')

## Dependencies

- `@packages/shared`: Shared types and utilities
- `hono`: Web framework

## Error Handling

The service includes comprehensive error handling for:
- Invalid city names
- Invalid unit specifications
- OpenWeatherMap API errors
- Network failures
- Invalid input validation

All errors are properly logged and return appropriate HTTP status codes with descriptive messages.

## Weather Data Units

The service supports two unit systems:
- `metric`: Temperature in Celsius, wind speed in meters/sec
- `imperial`: Temperature in Fahrenheit, wind speed in miles/hour

## TypeScript Support

The project is fully typed with TypeScript, providing excellent IDE support and type safety. The codebase includes type definitions for:
- API request/response structures
- Environment configurations
- Weather data models
- Error handling 
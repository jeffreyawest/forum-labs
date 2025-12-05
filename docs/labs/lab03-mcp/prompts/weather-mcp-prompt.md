# Weather MCP Server Prompt

**API**: OpenWeatherMap  
**Source App**: Weather App  
**Spec**: [weather-app-spec.md](../../../specs/weather-app-spec.md)

## Tools to Implement

| Tool | Description |
|------|-------------|
| `get_current_weather` | Get current conditions for a city |
| `get_forecast` | Get 5-day forecast |
| `get_air_quality` | Get air quality index |
| `compare_cities` | Compare weather between cities |

---

## Generation Prompt

Copy and paste this entire prompt to your AI assistant:

```
Create an MCP server in TypeScript that wraps the OpenWeatherMap API. Follow this specification:

## Project Setup

Create a new directory `weather-mcp-server` with these files:
- package.json
- tsconfig.json
- src/index.ts (main MCP server)

## Dependencies

{
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.0.0"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "typescript": "^5.0.0"
  }
}

## API Configuration

const API_KEY = '81208750b50a113806b890f45520281a';
const BASE_URL = 'https://api.openweathermap.org/data/2.5';

## Tools to Implement

### Tool 1: get_current_weather
- Description: Get current weather conditions for a city
- Parameters:
  - city (string, required): City name (e.g., "Seattle" or "London,UK")
  - units (string, optional): "metric" or "imperial", default "imperial"
- Returns: Object with temperature, feels_like, humidity, description, wind_speed, icon
- Endpoint: GET /weather?q={city}&units={units}&appid={API_KEY}

### Tool 2: get_forecast
- Description: Get 5-day weather forecast with 3-hour intervals
- Parameters:
  - city (string, required): City name
  - units (string, optional): "metric" or "imperial", default "imperial"
- Returns: Array of forecast items with dt_txt, temp, description, icon
- Endpoint: GET /forecast?q={city}&units={units}&appid={API_KEY}

### Tool 3: get_air_quality
- Description: Get air quality index for a location
- Parameters:
  - city (string, required): City name
- Returns: Object with aqi (1-5 scale), components (pm2_5, pm10, o3, no2)
- Flow: 
  1. First call /weather to get lat/lon for city
  2. Then call /air_pollution?lat={lat}&lon={lon}&appid={API_KEY}
- AQI labels: 1=Good, 2=Fair, 3=Moderate, 4=Poor, 5=Very Poor

### Tool 4: compare_cities
- Description: Compare current weather between multiple cities
- Parameters:
  - cities (string[], required): Array of city names (2-5 cities)
  - units (string, optional): "metric" or "imperial"
- Returns: Array of city weather objects for comparison
- Implementation: Call get_current_weather for each city in parallel

## Error Handling

- If city not found, return error message: "City not found: {city}"
- If API rate limited, return: "API rate limit exceeded. Try again later."
- Wrap all API calls in try/catch

## MCP Server Structure

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "weather-mcp-server",
  version: "1.0.0"
}, {
  capabilities: {
    tools: {}
  }
});

// Register tools using server.setRequestHandler for "tools/list" and "tools/call"

## Response Format

All tools should return well-formatted data that's easy for an AI to summarize:

{
  "success": true,
  "data": { ... },
  "summary": "Current weather in Seattle: 52°F, cloudy"
}

Generate the complete MCP server with all tools implemented.
```

---

## Test Prompts

After configuring your MCP server, try these prompts in GitHub Copilot Chat:

- "What's the weather in Tokyo?"
- "Get the 5-day forecast for Seattle"
- "What's the air quality in Los Angeles?"
- "Compare the weather in Seattle, Portland, and San Francisco"

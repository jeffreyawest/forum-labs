# Country Explorer MCP Server Prompt

**API**: REST Countries  
**Source App**: Country Explorer  
**Spec**: [country-explorer-spec.md](../../../specs/country-explorer-spec.md)

## Tools to Implement

| Tool | Description |
|------|-------------|
| `get_country` | Get country details by name |
| `search_countries` | Search countries by partial name |
| `get_countries_by_region` | List countries in a region |
| `get_country_neighbors` | Get bordering countries |
| `compare_countries` | Compare multiple countries |
| `get_travel_info` | Get travel-relevant information |

---

## Generation Prompt

Copy and paste this entire prompt to your AI assistant:

```
Create an MCP server in TypeScript that wraps the REST Countries API. Follow this specification:

## Project Setup

Create a new directory `countries-mcp-server` with these files:
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

const BASE_URL = 'https://restcountries.com/v3.1';
// No API key required

## Tools to Implement

### Tool 1: get_country
- Description: Get detailed information about a country
- Parameters:
  - name (string, required): Country name (common or official)
- Returns: Object with:
  {
    name: { common: "Japan", official: "Japan" },
    capital: "Tokyo",
    region: "Asia",
    subregion: "Eastern Asia",
    population: 125836021,
    area: 377930,
    languages: ["Japanese"],
    currencies: [{ name: "Japanese yen", symbol: "¥" }],
    timezones: ["UTC+09:00"],
    borders: ["none - island nation"],
    flag: "🇯🇵",
    drivingSide: "left",
    callingCode: "+81"
  }
- Endpoint: GET /name/{name}?fullText=true
- Fallback: GET /name/{name} if exact match fails

### Tool 2: search_countries
- Description: Search countries by partial name
- Parameters:
  - query (string, required): Partial name to search
- Returns: Array of matching countries with name, capital, region, flag
- Endpoint: GET /name/{query}
- Returns first 10 results

### Tool 3: get_countries_by_region
- Description: Get all countries in a region
- Parameters:
  - region (string, required): Region name (Africa, Americas, Asia, Europe, Oceania)
- Returns: Array of countries with name, capital, population, flag
- Endpoint: GET /region/{region}
- Sort by population descending

### Tool 4: get_country_neighbors
- Description: Get information about bordering countries
- Parameters:
  - country (string, required): Country name
- Returns: Object with:
  {
    country: "Germany",
    borderCount: 9,
    borders: [
      { name: "France", capital: "Paris", population: 67390000 },
      { name: "Poland", capital: "Warsaw", population: 37950000 },
      ...
    ]
  }
- Implementation:
  1. Get country to find border codes (cca3)
  2. Fetch each border country: GET /alpha/{code}
  3. Format results

### Tool 5: compare_countries
- Description: Compare statistics between countries
- Parameters:
  - countries (string[], required): Array of country names (2-5)
- Returns: Comparison table:
  {
    countries: ["USA", "China", "India"],
    comparison: {
      population: [331002651, 1439323776, 1380004385],
      area: [9833520, 9596960, 3287263],
      density: [33.7, 150.0, 419.9],
      languages: [["English"], ["Chinese"], ["Hindi", "English"]],
      currencies: ["USD ($)", "CNY (¥)", "INR (₹)"]
    },
    rankings: {
      largestPopulation: "China",
      largestArea: "USA",
      mostLanguages: "India"
    }
  }

### Tool 6: get_travel_info
- Description: Get travel-relevant information for a country
- Parameters:
  - country (string, required): Country name
- Returns: Object with:
  {
    country: "Japan",
    essentials: {
      capital: "Tokyo",
      languages: ["Japanese"],
      currency: { name: "Japanese yen", symbol: "¥", code: "JPY" },
      callingCode: "+81",
      drivingSide: "left",
      timezones: ["UTC+09:00"]
    },
    geography: {
      region: "Asia",
      subregion: "Eastern Asia",
      area: "377,930 km²",
      borders: "Island nation - no land borders"
    },
    links: {
      googleMaps: "https://...",
      openStreetMaps: "https://..."
    }
  }

## Error Handling

- If country not found (404), return: "Country not found: {name}"
- If region invalid, return: "Invalid region. Use: Africa, Americas, Asia, Europe, Oceania"
- Wrap all API calls in try/catch

## Formatting Helpers

function formatPopulation(num) {
  if (num >= 1e9) return (num / 1e9).toFixed(2) + ' billion';
  if (num >= 1e6) return (num / 1e6).toFixed(2) + ' million';
  return num.toLocaleString();
}

function formatArea(km2) {
  return km2.toLocaleString() + ' km²';
}

## MCP Server Structure

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "countries-mcp-server",
  version: "1.0.0"
}, {
  capabilities: {
    tools: {}
  }
});

## Response Format

{
  "success": true,
  "data": { ... },
  "summary": "Japan - 125.8 million people, capital Tokyo"
}

Generate the complete MCP server with all tools implemented.
```

---

## Test Prompts

After configuring your MCP server, try these prompts in GitHub Copilot Chat:

- "Tell me about Japan"
- "Search for countries starting with 'New'"
- "List all countries in Europe"
- "What countries border Germany?"
- "Compare the populations of USA, China, and India"
- "What do I need to know for traveling to France?"

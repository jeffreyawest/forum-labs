# Movie Tracker MCP Server Prompt

**API**: OMDb  
**Source App**: Movie & TV Tracker  
**Spec**: [movie-tv-tracker-spec.md](../../../specs/movie-tv-tracker-spec.md)

## Tools to Implement

| Tool | Description |
|------|-------------|
| `search_titles` | Search movies or TV shows |
| `get_title_details` | Get full details by IMDb ID |
| `get_title_by_name` | Get details by exact title |
| `get_ratings` | Get all ratings (IMDb, RT, Metacritic) |
| `compare_titles` | Compare multiple movies/shows |

---

## Generation Prompt

Copy and paste this entire prompt to your AI assistant:

```
Create an MCP server in TypeScript that wraps the OMDb API. Follow this specification:

## Project Setup

Create a new directory `omdb-mcp-server` with these files:
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

const API_KEY = 'YOUR_OMDB_API_KEY'; // User must replace
const BASE_URL = 'https://www.omdbapi.com/';

## Tools to Implement

### Tool 1: search_titles
- Description: Search for movies or TV shows by title
- Parameters:
  - query (string, required): Search term
  - type (string, optional): "movie" or "series", default both
  - year (string, optional): Release year to filter
  - page (number, optional): Page number for pagination, default 1
- Returns: Array of results with title, year, imdbID, type, poster
- Endpoint: GET /?s={query}&type={type}&y={year}&page={page}&apikey={API_KEY}

### Tool 2: get_title_details
- Description: Get full details for a movie or TV show by IMDb ID
- Parameters:
  - imdbId (string, required): IMDb ID (e.g., "tt0133093")
  - plot (string, optional): "short" or "full", default "full"
- Returns: Object with title, year, rated, released, runtime, genre, director, actors, plot, ratings array, poster, imdbRating, type, totalSeasons (for series)
- Endpoint: GET /?i={imdbId}&plot={plot}&apikey={API_KEY}

### Tool 3: get_title_by_name
- Description: Get details by exact title name
- Parameters:
  - title (string, required): Exact movie/show title
  - year (string, optional): Year to disambiguate
  - type (string, optional): "movie" or "series"
- Returns: Same format as get_title_details
- Endpoint: GET /?t={title}&y={year}&type={type}&apikey={API_KEY}

### Tool 4: get_ratings
- Description: Get all available ratings for a title
- Parameters:
  - imdbId (string, required): IMDb ID
- Returns: Object with:
  {
    imdb: { score: "8.7", votes: "1,900,000" },
    rottenTomatoes: { score: "88%" },
    metacritic: { score: "73/100" }
  }
- Note: Parse from Ratings array in API response

### Tool 5: compare_titles
- Description: Compare multiple movies or TV shows
- Parameters:
  - imdbIds (string[], required): Array of IMDb IDs (2-5)
- Returns: Comparison table with:
  {
    titles: ["The Matrix", "Inception"],
    comparison: {
      year: ["1999", "2010"],
      runtime: ["136 min", "148 min"],
      imdbRating: ["8.7", "8.8"],
      genre: ["Action, Sci-Fi", "Action, Sci-Fi, Thriller"],
      director: ["Wachowskis", "Christopher Nolan"]
    },
    winner: { imdbRating: "Inception (8.8)" }
  }

## Error Handling

- If Response: "False", return error from API: response.Error
- Common errors: "Movie not found!", "Invalid API key!"
- If API rate limited (402), return: "API limit exceeded"

## MCP Server Structure

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "omdb-mcp-server",
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
  "summary": "The Matrix (1999) - IMDb: 8.7/10"
}

Generate the complete MCP server with all tools implemented.
```

---

## Test Prompts

After configuring your MCP server, try these prompts in GitHub Copilot Chat:

- "Search for sci-fi movies from 1999"
- "Get details for The Matrix"
- "Find TV shows about dragons"
- "What are the ratings for Inception?"
- "Compare ratings for Inception and Interstellar"

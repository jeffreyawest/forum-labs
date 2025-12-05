# Lab 3: MCPify Your App

> **Duration**: 45-60 minutes  
> **Goal**: Create an MCP server that exposes your app's API as tools  
> **Prerequisites**: Completed Lab 1 or Lab 2 with a working app

---

## What is an MCP Facade?

An **MCP (Model Context Protocol) facade** wraps an existing API to expose it as tools that AI assistants can use. Instead of writing code to call APIs, you can ask your AI assistant to perform actions directly.

### Before MCP
```
User: "What's the weather in Seattle?"
AI: "I'll help you write code to call the OpenWeatherMap API..."
```

### After MCP
```
User: "What's the weather in Seattle?"
AI: [calls get_weather tool] "It's currently 52°F and cloudy in Seattle."
```

---

## Choose Your MCP Server

Based on the app you built in Labs 1-2, select the corresponding MCP server prompt below. Each prompt file includes:

1. **Overview** of tools to implement
2. **Complete prompt** to generate the MCP server
3. **Test prompts** to verify it works

| Option | App | API | Prompt File |
|--------|-----|-----|-------------|
| A | Weather App | OpenWeatherMap | [weather-mcp-prompt.md](prompts/weather-mcp-prompt.md) |
| B | Meal Planner | TheMealDB | [meal-planner-mcp-prompt.md](prompts/meal-planner-mcp-prompt.md) |
| C | Movie Tracker | OMDb | [movie-tracker-mcp-prompt.md](prompts/movie-tracker-mcp-prompt.md) |
| D | Pokémon Team Builder | PokéAPI | [pokemon-mcp-prompt.md](prompts/pokemon-mcp-prompt.md) |
| E | Country Explorer | REST Countries | [country-explorer-mcp-prompt.md](prompts/country-explorer-mcp-prompt.md) |

---

## Quick Reference: Tools by App

### Weather MCP Server
| Tool | Description |
|------|-------------|
| `get_current_weather` | Get current conditions for a city |
| `get_forecast` | Get 5-day forecast |
| `get_air_quality` | Get air quality index |
| `compare_cities` | Compare weather between cities |

### Meal Planner MCP Server
| Tool | Description |
|------|-------------|
| `search_recipes` | Search meals by name |
| `get_recipe_details` | Get full recipe with ingredients |
| `get_random_recipe` | Get a random meal suggestion |
| `list_categories` | List all meal categories |
| `get_recipes_by_category` | Get meals in a category |
| `generate_shopping_list` | Create shopping list from meal IDs |

### Movie Tracker MCP Server
| Tool | Description |
|------|-------------|
| `search_titles` | Search movies or TV shows |
| `get_title_details` | Get full details by IMDb ID |
| `get_title_by_name` | Get details by exact title |
| `get_ratings` | Get all ratings (IMDb, RT, Metacritic) |
| `compare_titles` | Compare multiple movies/shows |

### Pokémon MCP Server
| Tool | Description |
|------|-------------|
| `get_pokemon` | Get Pokémon details by name or ID |
| `search_pokemon` | Search Pokémon by partial name |
| `get_pokemon_by_type` | List Pokémon of a specific type |
| `get_type_effectiveness` | Get type matchup data |
| `analyze_team` | Analyze team strengths/weaknesses |
| `suggest_pokemon` | Suggest Pokémon to fill team gaps |

### Country Explorer MCP Server
| Tool | Description |
|------|-------------|
| `get_country` | Get country details by name |
| `search_countries` | Search countries by partial name |
| `get_countries_by_region` | List countries in a region |
| `get_country_neighbors` | Get bordering countries |
| `compare_countries` | Compare multiple countries |
| `get_travel_info` | Get travel-relevant information |

---

## After Generation

### Step 1: Install Dependencies

```bash
cd your-mcp-server
npm install
```

### Step 2: Build the Server

```bash
npm run build
# or
npx tsc
```

### Step 3: Test Locally

```bash
node dist/index.js
```

### Step 4: Configure in VS Code

Add to your VS Code settings or `mcp.json`:

```json
{
  "mcpServers": {
    "your-server-name": {
      "command": "node",
      "args": ["path/to/your-mcp-server/dist/index.js"]
    }
  }
}
```

### Step 5: Test with Copilot

Refer to the test prompts in your chosen prompt file to verify your MCP server works correctly.

---

## Extending Your MCP Server

### Add Resources

Resources let AI read data from your server:

```typescript
server.setRequestHandler(ListResourcesRequestSchema, async () => ({
  resources: [
    {
      uri: "weather://favorites",
      name: "Favorite Cities",
      description: "Your saved weather locations"
    }
  ]
}));
```

### Add Prompts

Prompts provide reusable templates:

```typescript
server.setRequestHandler(ListPromptsRequestSchema, async () => ({
  prompts: [
    {
      name: "weekly_meal_plan",
      description: "Generate a week of meal suggestions",
      arguments: [
        { name: "dietary_restrictions", description: "Any dietary restrictions", required: false }
      ]
    }
  ]
}));
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Module not found" | Run `npm install` |
| "Cannot find module '@modelcontextprotocol/sdk'" | Ensure package.json has correct dependency |
| Tools not appearing | Check server registration and capabilities |
| API errors | Verify API key and network access |
| TypeScript errors | Run `npx tsc --noEmit` to check types |

---

## Summary

You've learned how to:

1. ✅ Identify tools to expose from an existing API
2. ✅ Generate an MCP server using a comprehensive prompt
3. ✅ Configure the server for use with VS Code
4. ✅ Test tools with natural language queries

**Key Insight**: MCP servers turn any API into a natural language interface. The same weather API that required code now responds to "What's the weather?"

---

## Next Steps

- **Lab 4**: Learn about PLAN mode for complex multi-step tasks
- **Advanced**: Add caching, rate limiting, or authentication to your MCP server
- **Explore**: Combine multiple MCP servers for cross-domain queries

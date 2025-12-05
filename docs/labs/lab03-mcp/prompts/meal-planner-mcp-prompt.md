# Meal Planner MCP Server Prompt

**API**: TheMealDB  
**Source App**: Meal Planner  
**Spec**: [meal-planner-spec.md](../../../specs/meal-planner-spec.md)

## Tools to Implement

| Tool | Description |
|------|-------------|
| `search_recipes` | Search meals by name |
| `get_recipe_details` | Get full recipe with ingredients |
| `get_random_recipe` | Get a random meal suggestion |
| `list_categories` | List all meal categories |
| `get_recipes_by_category` | Get meals in a category |
| `generate_shopping_list` | Create shopping list from meal IDs |

---

## Generation Prompt

Copy and paste this entire prompt to your AI assistant:

```
Create an MCP server in TypeScript that wraps TheMealDB API. Follow this specification:

## Project Setup

Create a new directory `mealdb-mcp-server` with these files:
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

const BASE_URL = 'https://www.themealdb.com/api/json/v1/1';
// No API key required for TheMealDB

## Tools to Implement

### Tool 1: search_recipes
- Description: Search for meals by name
- Parameters:
  - query (string, required): Search term (e.g., "chicken", "pasta")
- Returns: Array of meals with id, name, category, area, thumbnail
- Endpoint: GET /search.php?s={query}
- Note: Returns null meals array if no results

### Tool 2: get_recipe_details
- Description: Get full recipe details including ingredients and instructions
- Parameters:
  - id (string, required): Meal ID from search results
- Returns: Object with name, category, area, instructions, ingredients (parsed array), thumbnail
- Endpoint: GET /lookup.php?i={id}
- Parsing: Extract strIngredient1-20 and strMeasure1-20 into array of {ingredient, measure}
- Filter out empty ingredients

### Tool 3: get_random_recipe
- Description: Get a random meal suggestion
- Parameters: none
- Returns: Same format as get_recipe_details
- Endpoint: GET /random.php

### Tool 4: list_categories
- Description: List all available meal categories
- Parameters: none
- Returns: Array of categories with name, thumbnail, description
- Endpoint: GET /categories.php

### Tool 5: get_recipes_by_category
- Description: Get all meals in a specific category
- Parameters:
  - category (string, required): Category name (e.g., "Seafood", "Vegetarian")
- Returns: Array of meals with id, name, thumbnail
- Endpoint: GET /filter.php?c={category}

### Tool 6: generate_shopping_list
- Description: Generate aggregated shopping list from multiple meals
- Parameters:
  - mealIds (string[], required): Array of meal IDs to include
- Returns: Object with categorized ingredients:
  {
    proteins: [{ingredient, measures: []}],
    produce: [{ingredient, measures: []}],
    dairy: [{ingredient, measures: []}],
    pantry: [{ingredient, measures: []}],
    spices: [{ingredient, measures: []}],
    other: [{ingredient, measures: []}]
  }
- Implementation:
  1. Fetch details for each meal ID
  2. Extract all ingredients
  3. Combine duplicates (same ingredient = combine measures)
  4. Categorize using keyword matching:
     - proteins: chicken, beef, pork, fish, salmon, shrimp, lamb, egg
     - produce: onion, garlic, tomato, pepper, carrot, lettuce, potato
     - dairy: milk, cheese, butter, cream, yogurt
     - pantry: flour, sugar, rice, pasta, oil, vinegar, bread
     - spices: salt, pepper, paprika, cumin, oregano, basil

## Error Handling

- If meal not found, return: "No meals found for: {query}"
- If category invalid, return: "Invalid category: {category}"
- Wrap all API calls in try/catch

## MCP Server Structure

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "mealdb-mcp-server",
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
  "summary": "Found 5 chicken recipes"
}

Generate the complete MCP server with all tools implemented.
```

---

## Test Prompts

After configuring your MCP server, try these prompts in GitHub Copilot Chat:

- "Find me some chicken recipes"
- "What ingredients do I need for meal 52772?"
- "Get me a random recipe suggestion"
- "What meal categories are available?"
- "Show me vegetarian recipes"
- "Generate a shopping list for pasta carbonara and chicken teriyaki"

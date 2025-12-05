# Pokémon Team Builder MCP Server Prompt

**API**: PokéAPI  
**Source App**: Pokémon Team Builder  
**Spec**: [pokemon-team-builder-spec.md](../../../specs/pokemon-team-builder-spec.md)

## Tools to Implement

| Tool | Description |
|------|-------------|
| `get_pokemon` | Get Pokémon details by name or ID |
| `search_pokemon` | Search Pokémon by partial name |
| `get_pokemon_by_type` | List Pokémon of a specific type |
| `get_type_effectiveness` | Get type matchup data |
| `analyze_team` | Analyze team strengths/weaknesses |
| `suggest_pokemon` | Suggest Pokémon to fill team gaps |

---

## Generation Prompt

Copy and paste this entire prompt to your AI assistant:

```
Create an MCP server in TypeScript that wraps the PokéAPI. Follow this specification:

## Project Setup

Create a new directory `pokeapi-mcp-server` with these files:
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

const BASE_URL = 'https://pokeapi.co/api/v2';
// No API key required

## Type Colors (for reference in responses)

const TYPE_COLORS = {
  normal: '#A8A878', fire: '#F08030', water: '#6890F0',
  electric: '#F8D030', grass: '#78C850', ice: '#98D8D8',
  fighting: '#C03028', poison: '#A040A0', ground: '#E0C068',
  flying: '#A890F0', psychic: '#F85888', bug: '#A8B820',
  rock: '#B8A038', ghost: '#705898', dragon: '#7038F8',
  dark: '#705848', steel: '#B8B8D0', fairy: '#EE99AC'
};

## Tools to Implement

### Tool 1: get_pokemon
- Description: Get detailed information about a Pokémon
- Parameters:
  - nameOrId (string, required): Pokémon name or Pokédex number
- Returns: Object with:
  {
    id: 25,
    name: "pikachu",
    types: ["electric"],
    stats: { hp: 35, attack: 55, defense: 40, spAtk: 50, spDef: 50, speed: 90 },
    abilities: ["static", "lightning-rod (hidden)"],
    height: "0.4m",
    weight: "6.0kg",
    sprite: "https://..."
  }
- Endpoint: GET /pokemon/{nameOrId}
- Parse stats from stats array, convert height/10 to meters, weight/10 to kg

### Tool 2: search_pokemon
- Description: Search Pokémon by partial name match
- Parameters:
  - query (string, required): Partial name to search
  - limit (number, optional): Max results, default 10
- Returns: Array of matching Pokémon with id, name
- Implementation: 
  1. Fetch /pokemon?limit=1010 (all Pokémon)
  2. Filter results.name.includes(query.toLowerCase())
  3. Return first {limit} matches

### Tool 3: get_pokemon_by_type
- Description: Get all Pokémon of a specific type
- Parameters:
  - type (string, required): Type name (e.g., "fire", "water")
  - limit (number, optional): Max results, default 20
- Returns: Array of Pokémon with id, name, slot (primary/secondary)
- Endpoint: GET /type/{type}
- Parse from pokemon array in response

### Tool 4: get_type_effectiveness
- Description: Get type matchup information
- Parameters:
  - type (string, required): Type name
- Returns: Object with:
  {
    type: "fire",
    offensive: {
      superEffective: ["grass", "ice", "bug", "steel"],
      notVeryEffective: ["fire", "water", "rock", "dragon"],
      noEffect: []
    },
    defensive: {
      weakTo: ["water", "ground", "rock"],
      resistantTo: ["fire", "grass", "ice", "bug", "steel", "fairy"],
      immuneTo: []
    }
  }
- Endpoint: GET /type/{type}
- Parse from damage_relations in response

### Tool 5: analyze_team
- Description: Analyze a team's type coverage and weaknesses
- Parameters:
  - pokemon (string[], required): Array of Pokémon names (1-6)
- Returns: Object with:
  {
    team: ["pikachu", "charizard", "blastoise"],
    typesCovered: ["electric", "fire", "flying", "water"],
    weaknesses: {
      "4x": [],
      "2x": ["rock", "electric", "ground"]
    },
    resistances: {
      "0.25x": ["fire"],
      "0.5x": ["grass", "steel", "bug", "ice", "fairy"]
    },
    immunities: ["ground"],
    coverage: {
      superEffective: ["water", "flying", "ground", "rock", "grass", "ice", "bug", "steel"],
      gaps: ["electric", "dragon"]
    }
  }
- Implementation:
  1. Fetch each Pokémon's types
  2. Fetch type effectiveness for each type
  3. Calculate combined weaknesses (multiply for dual types)
  4. Calculate offensive coverage

### Tool 6: suggest_pokemon
- Description: Suggest Pokémon to fill gaps in a team
- Parameters:
  - currentTeam (string[], required): Current team members
  - preferredType (string, optional): Type preference
- Returns: Array of suggestions with:
  {
    pokemon: "rhydon",
    types: ["ground", "rock"],
    reason: "Covers electric weakness, resists rock"
  }
- Implementation:
  1. Analyze current team weaknesses
  2. Find Pokémon that resist those types
  3. Prioritize Pokémon that also provide offensive coverage gaps

## Error Handling

- If Pokémon not found (404), return: "Pokémon not found: {name}"
- If type invalid, return: "Invalid type: {type}"
- Valid types: normal, fire, water, electric, grass, ice, fighting, poison, ground, flying, psychic, bug, rock, ghost, dragon, dark, steel, fairy

## MCP Server Structure

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "pokeapi-mcp-server",
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
  "summary": "Pikachu (#25) - Electric type, 90 Speed"
}

Generate the complete MCP server with all tools implemented.
```

---

## Test Prompts

After configuring your MCP server, try these prompts in GitHub Copilot Chat:

- "Tell me about Pikachu's stats"
- "Search for Pokémon with 'char' in their name"
- "List fire type Pokémon"
- "What are fire type's weaknesses and strengths?"
- "Analyze a team of Charizard, Blastoise, and Venusaur"
- "Suggest a Pokémon to add to my team of Pikachu and Eevee"

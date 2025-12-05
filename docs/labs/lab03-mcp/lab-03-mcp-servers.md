# Lab 3: MCP Server Development and Configuration

## 🎯 Objective

Learn to extend AI capabilities by creating and configuring Model Context Protocol (MCP) servers. You'll build a custom MCP server that provides weather data context, and configure existing MCP servers for Azure DevOps integration.

**Time:** 45 minutes

---

## Learning Goals

By the end of this lab, you will:
- ✅ Understand the MCP protocol and its purpose
- ✅ Create a custom MCP server from scratch
- ✅ Expose APIs as AI-accessible tools
- ✅ Configure pre-built MCP servers (ADO, etc.)
- ✅ Use MCP servers with Cline/Copilot

---

## What is MCP?

### Model Context Protocol

MCP is an open protocol that enables AI assistants to:

```
┌─────────────────┐         ┌─────────────────┐
│   AI Assistant  │◄───────►│   MCP Server    │
│  (Cline/Copilot)│  JSON   │  (Your Tools)   │
└─────────────────┘  RPC    └─────────────────┘
                               │
                               ▼
                        ┌─────────────────┐
                        │  External Data  │
                        │  - APIs         │
                        │  - Databases    │
                        │  - Files        │
                        │  - Services     │
                        └─────────────────┘
```

### Key Concepts

| Concept | Description |
|---------|-------------|
| **Tools** | Functions the AI can call (e.g., `get_weather`) |
| **Resources** | Data the AI can read (e.g., documentation) |
| **Prompts** | Pre-built prompt templates |

---

## Part A: Create an MCP Server (25 minutes)

### Setup

Create a new project:

```bash
mkdir weather-mcp-server
cd weather-mcp-server
npm init -y
```

### Step 1: Install Dependencies

```bash
npm install @modelcontextprotocol/sdk zod
npm install -D typescript @types/node tsx
```

### Step 2: Create TypeScript Configuration

Create `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "Node16",
    "moduleResolution": "Node16",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "declaration": true
  },
  "include": ["src/**/*"]
}
```

### Step 3: Create the MCP Server

Create `src/index.ts`:

```typescript
#!/usr/bin/env node

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
  ListResourcesRequestSchema,
  ReadResourceRequestSchema,
} from "@modelcontextprotocol/sdk/types.js";
import { z } from "zod";

// Configuration
const API_KEY = process.env.OPENWEATHER_API_KEY || "YOUR_API_KEY";
const BASE_URL = "https://api.openweathermap.org/data/2.5";

// Types
interface WeatherData {
  name: string;
  country: string;
  temp: number;
  feels_like: number;
  humidity: number;
  wind_speed: number;
  description: string;
  icon: string;
}

interface ForecastDay {
  date: string;
  temp_high: number;
  temp_low: number;
  description: string;
}

// API Functions
async function fetchWeather(location: string): Promise<WeatherData> {
  const isZip = /^\d{5}$/.test(location);
  const param = isZip ? `zip=${location},US` : `q=${encodeURIComponent(location)}`;
  
  const url = `${BASE_URL}/weather?${param}&appid=${API_KEY}&units=imperial`;
  const response = await fetch(url);
  
  if (!response.ok) {
    throw new Error(`Weather API error: ${response.statusText}`);
  }
  
  const data = await response.json();
  
  return {
    name: data.name,
    country: data.sys.country,
    temp: Math.round(data.main.temp),
    feels_like: Math.round(data.main.feels_like),
    humidity: data.main.humidity,
    wind_speed: Math.round(data.wind.speed),
    description: data.weather[0].description,
    icon: data.weather[0].icon,
  };
}

async function fetchForecast(location: string): Promise<ForecastDay[]> {
  const isZip = /^\d{5}$/.test(location);
  const param = isZip ? `zip=${location},US` : `q=${encodeURIComponent(location)}`;
  
  const url = `${BASE_URL}/forecast?${param}&appid=${API_KEY}&units=imperial`;
  const response = await fetch(url);
  
  if (!response.ok) {
    throw new Error(`Forecast API error: ${response.statusText}`);
  }
  
  const data = await response.json();
  
  // Group by day and get daily highs/lows
  const dailyMap = new Map<string, { temps: number[]; description: string }>();
  
  for (const item of data.list) {
    const date = new Date(item.dt * 1000).toLocaleDateString();
    if (!dailyMap.has(date)) {
      dailyMap.set(date, { temps: [], description: item.weather[0].description });
    }
    dailyMap.get(date)!.temps.push(item.main.temp);
  }
  
  const forecast: ForecastDay[] = [];
  dailyMap.forEach((value, date) => {
    forecast.push({
      date,
      temp_high: Math.round(Math.max(...value.temps)),
      temp_low: Math.round(Math.min(...value.temps)),
      description: value.description,
    });
  });
  
  return forecast.slice(0, 5);
}

// Create MCP Server
const server = new Server(
  {
    name: "weather-mcp",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
      resources: {},
    },
  }
);

// Define Tools
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "get_current_weather",
        description: "Get current weather conditions for a city or zip code",
        inputSchema: {
          type: "object",
          properties: {
            location: {
              type: "string",
              description: "City name (e.g., 'Seattle') or US zip code (e.g., '98101')",
            },
          },
          required: ["location"],
        },
      },
      {
        name: "get_forecast",
        description: "Get 5-day weather forecast for a city or zip code",
        inputSchema: {
          type: "object",
          properties: {
            location: {
              type: "string",
              description: "City name (e.g., 'Seattle') or US zip code (e.g., '98101')",
            },
          },
          required: ["location"],
        },
      },
      {
        name: "compare_weather",
        description: "Compare weather between two locations",
        inputSchema: {
          type: "object",
          properties: {
            location1: {
              type: "string",
              description: "First city or zip code",
            },
            location2: {
              type: "string",
              description: "Second city or zip code",
            },
          },
          required: ["location1", "location2"],
        },
      },
    ],
  };
});

// Handle Tool Calls
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  const { name, arguments: args } = request.params;

  try {
    switch (name) {
      case "get_current_weather": {
        const location = (args as { location: string }).location;
        const weather = await fetchWeather(location);
        return {
          content: [
            {
              type: "text",
              text: JSON.stringify(weather, null, 2),
            },
          ],
        };
      }

      case "get_forecast": {
        const location = (args as { location: string }).location;
        const forecast = await fetchForecast(location);
        return {
          content: [
            {
              type: "text",
              text: JSON.stringify(forecast, null, 2),
            },
          ],
        };
      }

      case "compare_weather": {
        const { location1, location2 } = args as {
          location1: string;
          location2: string;
        };
        const [weather1, weather2] = await Promise.all([
          fetchWeather(location1),
          fetchWeather(location2),
        ]);
        return {
          content: [
            {
              type: "text",
              text: JSON.stringify(
                {
                  comparison: {
                    [weather1.name]: weather1,
                    [weather2.name]: weather2,
                  },
                  tempDifference: weather1.temp - weather2.temp,
                },
                null,
                2
              ),
            },
          ],
        };
      }

      default:
        throw new Error(`Unknown tool: ${name}`);
    }
  } catch (error) {
    return {
      content: [
        {
          type: "text",
          text: `Error: ${error instanceof Error ? error.message : "Unknown error"}`,
        },
      ],
      isError: true,
    };
  }
});

// Define Resources
server.setRequestHandler(ListResourcesRequestSchema, async () => {
  return {
    resources: [
      {
        uri: "weather://api-docs",
        name: "Weather API Documentation",
        description: "Documentation for the weather MCP tools",
        mimeType: "text/markdown",
      },
    ],
  };
});

server.setRequestHandler(ReadResourceRequestSchema, async (request) => {
  if (request.params.uri === "weather://api-docs") {
    return {
      contents: [
        {
          uri: "weather://api-docs",
          mimeType: "text/markdown",
          text: `# Weather MCP Server

## Tools

### get_current_weather
Get current weather for any location.
- Input: location (city name or zip code)
- Returns: temp, humidity, wind, description

### get_forecast
Get 5-day forecast.
- Input: location
- Returns: Array of daily forecasts

### compare_weather
Compare weather between two locations.
- Input: location1, location2
- Returns: Both weather reports + temperature difference

## Examples

"What's the weather in Seattle?"
"Compare the weather between New York and Los Angeles"
"Get the 5-day forecast for 98101"
`,
        },
      ],
    };
  }
  throw new Error("Resource not found");
});

// Start Server
async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("Weather MCP Server running on stdio");
}

main().catch(console.error);
```

### Step 4: Update package.json

Update your `package.json`:

```json
{
  "name": "weather-mcp-server",
  "version": "1.0.0",
  "type": "module",
  "bin": {
    "weather-mcp": "./dist/index.js"
  },
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "tsx src/index.ts"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^0.5.0",
    "zod": "^3.22.0"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "tsx": "^4.0.0",
    "typescript": "^5.0.0"
  }
}
```

### Step 5: Build and Test

```bash
npm run build
```

---

## Part B: Configure the MCP Server (10 minutes)

### Step 1: Configure in Cline

Open VS Code settings or Cline's MCP configuration file.

**For Cline (cline_mcp_settings.json):**

Find the settings file location:
- Windows: `%APPDATA%\Code\User\globalStorage\saoudrizwan.claude-dev\settings\cline_mcp_settings.json`
- Mac: `~/Library/Application Support/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json`

Add your server configuration:

```json
{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": ["C:/path/to/weather-mcp-server/dist/index.js"],
      "env": {
        "OPENWEATHER_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Step 2: Verify the Connection

In Cline, you should now see the weather tools available. Test with:

```
What's the weather in Seattle?
```

Cline should use your `get_current_weather` tool!

---

## Part C: Configure Existing MCP Servers (10 minutes)

### Azure DevOps MCP Server

If you have Azure DevOps access, you can configure the ADO MCP server:

```json
{
  "mcpServers": {
    "azure-devops": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-azure-devops"],
      "env": {
        "AZURE_DEVOPS_ORG": "your-org",
        "AZURE_DEVOPS_PAT": "your-personal-access-token"
      }
    }
  }
}
```

### GitHub MCP Server

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```

### Filesystem MCP Server

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:/path/to/allowed/directory"
      ]
    }
  }
}
```

---

## 📊 Testing Your MCP Server

### Test Prompts

Try these with Cline to verify your MCP server works:

1. **Basic weather lookup:**
   ```
   What's the current weather in New York City?
   ```

2. **Forecast:**
   ```
   Give me the 5-day forecast for zip code 90210
   ```

3. **Comparison:**
   ```
   Compare the weather between Seattle and Miami
   ```

4. **Natural conversation:**
   ```
   I'm planning a trip. Is it warmer in Denver or Phoenix right now?
   ```

### Verification Checklist

- [ ] MCP server starts without errors
- [ ] Tools appear in Cline's tool list
- [ ] `get_current_weather` returns data
- [ ] `get_forecast` returns 5 days
- [ ] `compare_weather` works for two cities
- [ ] Error handling works for invalid locations

---

## 🔑 Key Takeaways

### MCP Benefits

1. **Extensibility** - Add any data source to your AI
2. **Separation of concerns** - Tools live outside the AI
3. **Reusability** - Same MCP server works with any MCP client
4. **Security** - Control what the AI can access

### When to Create MCP Servers

| Scenario | MCP Server? |
|----------|-------------|
| Access company APIs | ✅ Yes |
| Query internal databases | ✅ Yes |
| Integrate with external services | ✅ Yes |
| One-off data lookup | ❌ Maybe not worth it |
| Static documentation | ❌ Use context files instead |

### MCP Architecture Patterns

```
Pattern 1: Direct API Wrapper
┌─────────┐     ┌──────────┐     ┌─────────┐
│ Cline   │────►│ MCP      │────►│ Weather │
│         │     │ Server   │     │ API     │
└─────────┘     └──────────┘     └─────────┘

Pattern 2: Aggregator
┌─────────┐     ┌──────────┐     ┌─────────┐
│ Cline   │────►│ MCP      │────►│ API 1   │
│         │     │ Server   │────►│ API 2   │
│         │     │          │────►│ API 3   │
└─────────┘     └──────────┘     └─────────┘

Pattern 3: Data Transformer
┌─────────┐     ┌──────────┐     ┌─────────┐
│ Cline   │────►│ MCP      │────►│ Raw     │
│         │     │ (Transform)    │ Data    │
└─────────┘     └──────────┘     └─────────┘
```

---

## 🚀 Bonus Challenges

If you finish early:

### Challenge 1: Add a Tool
Add a `get_weather_alerts` tool that returns weather alerts for a location.

### Challenge 2: Add Caching
Cache weather responses for 5 minutes to reduce API calls.

### Challenge 3: Create a Different MCP Server
Ideas:
- **Dictionary MCP**: Look up word definitions
- **Stock MCP**: Get stock prices
- **News MCP**: Fetch headlines

---

## ✅ Completion Checklist

Before moving to Lab 4:

- [ ] Created a TypeScript MCP server
- [ ] Implemented at least 2 tools
- [ ] Configured the server in Cline
- [ ] Successfully called tools via Cline
- [ ] Understand the MCP architecture

---

## 📚 Resources

- [MCP Protocol Specification](https://modelcontextprotocol.io/)
- [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
- [MCP Server Examples](https://github.com/modelcontextprotocol/servers)
- [Cline MCP Documentation](https://github.com/cline/cline)

---

*Next: [Lab 4 - PLAN Mode & Memory Banks](../lab05-your-code/lab-05-plan-mode.md)*

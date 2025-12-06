# Agentic Programming Workshop

A hands-on workshop teaching participants how to leverage AI coding assistants (GitHub Copilot, Cline) for effective software development through structured prompting, context engineering, and tool integration.

## 🎯 Workshop Overview

This 4-hour workshop guides participants through the evolution from unstructured "vibe coding" to sophisticated agentic programming, demonstrating how proper context and tooling dramatically improve AI-assisted development outcomes.

### Learning Objectives

- ✅ Understand the difference between iterative prompting and structured agentic development
- ✅ Create effective specifications and context files for deterministic AI outputs
- ✅ Build and configure MCP (Model Context Protocol) servers for enhanced AI capabilities
- ✅ Use PLAN mode effectively for codebase exploration and informed development
- ✅ Build and maintain context stores/memory banks for ongoing projects

## 📋 Prerequisites

### Required Software
- VS Code (latest version)
- GitHub Copilot extension (with active subscription)
- Cline extension (latest version)
- Node.js 18+
- Git

### Recommended
- OpenWeatherMap API key (free tier) - [Get one here](https://openweathermap.org/api)
- Azure DevOps access (optional, for MCP configuration)
- Python 3.10+ (optional, for alternative implementations)

### Environment Verification
```bash
node --version    # Should be 18+
code --version    # VS Code installed
git --version     # Git installed
```

## 🗓️ Workshop Agenda

| Time | Duration | Session | Description |
|------|----------|---------|-------------|
| 0:00 | 15 min | **Introduction** | Welcome, objectives, and environment setup |
| 0:15 | 45 min | **[Lab 1: Vibe Coding](docs/labs/lab01-vibe-code/)** | Iterative prompting to build a Weather App |
| 1:00 | 10 min | **Break** | |
| 1:10 | 45 min | **[Lab 2: Spec-Driven Development](docs/labs/lab02-spec/)** | Same app with specs and engineered context |
| 1:55 | 15 min | **Debrief: Labs 1 vs 2** | Compare approaches, discuss learnings |
| 2:10 | 10 min | **Break** | |
| 2:20 | 45 min | **[Lab 3: MCP Servers](docs/labs/lab03-mcp/)** | Create and configure MCP servers |
| 3:05 | 10 min | **Break** | |
| 3:15 | 35 min | **[Lab 4: PLAN Mode & Memory](docs/labs/lab04-personas/)** | Intelligent codebase exploration |
| 3:50 | 10 min | **Wrap-up** | Q&A, resources, next steps |

**Total Duration: ~4 hours**

## 📚 Labs

### 🌊 Lab 1: Vibe Coding - The Iterative Approach
**Duration:** 45 minutes

Experience the challenges of unstructured AI-assisted development. Build an app using only high-level prompts and discover how iterative prompting without specifications leads to more iterations, inconsistent results, and missing requirements.

**Choose one of five app options:**

| App | Description | API | Key Required? |
|-----|-------------|-----|---------------|
| 🌤️ [Weather App](docs/labs/lab01-vibe-code/weather/) | Current conditions, 5-day forecast, 48-hour hourly forecast, sun position, and air quality data | OpenWeatherMap | Yes (free) |
| 🌍 [Country Explorer](docs/labs/lab01-vibe-code/country_explorer/) | Browse and search countries worldwide with details on population, languages, currencies, and borders | REST Countries | No |
| 🍽️ [Meal Planner](docs/labs/lab01-vibe-code/meal_planner/) | Search recipes, browse by category, view ingredients and instructions, plan weekly meals | TheMealDB | No |
| 🎮 [Pokemon Team Builder](docs/labs/lab01-vibe-code/pokemon_team_builder/) | Browse Pokémon, view stats/types/abilities, build and manage a team of 6, analyze team composition | PokéAPI | No |
| 🎬 [Movie/TV Tracker](docs/labs/lab01-vibe-code/movie_tv_tracker/) | Search movies and TV shows, view details and ratings, track watchlist and watched status | OMDb | Yes (free) |

> **All apps use Microsoft Fluent 2.0 design system and vanilla HTML/CSS/JavaScript (no frameworks).**

---

### 📋 Lab 2: Agentic Coding with Specs
**Duration:** 45 minutes

Build the **same app** from Lab 1 using detailed specifications, engineered context files, and Cline's "Deep Planning" feature. Compare time, iterations, and output quality with your Lab 1 experience.

**Detailed specifications available for each app:**

| App | Specification | What's Included |
|-----|---------------|-----------------|
| 🌤️ [Weather App](docs/specs/weather-app-spec.md) | Full UI mockups, API endpoints, Fluent 2.0 tokens, component specs |
| 🌍 [Country Explorer](docs/specs/country-explorer-spec.md) | Search/filter logic, detail views, comparison features, responsive layouts |
| 🍽️ [Meal Planner](docs/specs/meal-planner-spec.md) | Category browsing, recipe display, weekly planning, shopping list generation |
| 🎮 [Pokemon Team Builder](docs/specs/pokemon-team-builder-spec.md) | Pokémon cards, team slots, type coverage analysis, stat comparisons |
| 🎬 [Movie/TV Tracker](docs/specs/movie-tv-tracker-spec.md) | Search interface, detail modals, watchlist management, local storage |

---

### 🔌 Lab 3: MCP Server Development
**Duration:** 45 minutes

Learn to extend AI capabilities through custom context providers. Create an MCP server from scratch, expose API data as AI-accessible tools, and configure existing MCP servers.

📄 [Lab 3 Guide](docs/labs/lab03-mcp/lab-03-mcp-servers.md)

**Topics covered:**
- MCP protocol fundamentals
- Building TypeScript MCP servers
- Exposing APIs as AI tools
- Configuring pre-built MCP servers (Azure DevOps, GitHub)

---

### 🧠 Lab 4: PLAN Mode & Memory Banks
**Duration:** 35 minutes

Master intelligent codebase exploration and context management. Use Copilot/Cline in PLAN mode to ask informed questions, create memory banks, and build persistent context stores.

📄 [Lab 4 Guide](docs/labs/lab05-your-code/lab-05-plan-mode.md)

---

## 🏗️ Project Structure

```
forum-labs/
├── docs/
│   ├── AGENDA.md              # Detailed workshop agenda
│   ├── INDEX.md               # Documentation index
│   ├── labs/                  # Lab guides
│   │   ├── lab01-vibe-code/   # Lab 1: Five app options
│   │   ├── lab02-spec/        # Lab 2: Spec-driven development
│   │   ├── lab03-mcp/         # Lab 3: MCP servers
│   │   └── lab04-personas/    # Lab 4: PLAN mode (empty, see lab05)
│   │   └── lab05-your-code/   # Lab 4/5: Your code exercises
│   └── specs/                 # Detailed app specifications
│       ├── weather-app-spec.md
│       ├── meal-planner-spec.md
│       ├── movie-tv-tracker-spec.md
│       ├── pokemon-team-builder-spec.md
│       └── country-explorer-spec.md
└── src-mockup/                # Reference implementations
    └── meal-planner-mockup/
```

## 🎓 Key Concepts

### The Spectrum of AI-Assisted Development

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   VIBE CODING          STRUCTURED            AGENTIC                │
│   (Lab 1)              (Lab 2)               (Labs 3-4)             │
│                                                                      │
│   "Make it work"       "Here's the spec"     "Here's the context,   │
│                                               tools, and goals"      │
│                                                                      │
│   ❌ Unpredictable     ✅ Deterministic      ✅ Intelligent          │
│   ❌ Iterative         ✅ First-time right   ✅ Adaptive             │
│   ❌ Inconsistent      ✅ Consistent         ✅ Context-aware        │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### The Context Engineering Pyramid

```
                    ┌─────────────┐
                    │   TOOLS     │  ← MCP Servers, APIs
                    │   (Lab 3)   │
                    ├─────────────┤
                    │   MEMORY    │  ← Context stores, history
                    │   (Lab 4)   │
                    ├─────────────┤
                    │    SPECS    │  ← Requirements, constraints
                    │   (Lab 2)   │
                    ├─────────────┤
                    │   PROMPTS   │  ← Instructions, goals
                    │   (Lab 1)   │
                    └─────────────┘
```

## 🚀 Getting Started

1. **Clone this repository:**
   ```bash
   git clone <repository-url>
   cd forum-labs
   ```

2. **Verify your environment:**
   ```bash
   node --version
   code --version
   ```

3. **Get your API key:**
   - Sign up at [OpenWeatherMap](https://openweathermap.org/api) (free tier)
   - Save your API key for use in the labs

4. **Start with Lab 1:**
   - Choose one of the five app options
   - Follow the iterative prompting guide
   - Track your experience for comparison in Lab 2

## 📖 Documentation

- **[Full Agenda](docs/AGENDA.md)** - Detailed workshop schedule and session descriptions
- **[Document Index](docs/INDEX.md)** - Complete listing of all workshop materials
- **[Lab Guides](docs/labs/)** - Step-by-step instructions for each lab

## 🎯 Learning Outcomes

By completing this workshop, participants will:

1. **Understand trade-offs** between rapid "vibe coding" and structured development
2. **Write effective specifications** that enable AI assistants to generate better code
3. **Build MCP servers** to extend AI capabilities with custom tools and context
4. **Use PLAN mode** to intelligently explore and understand existing codebases
5. **Create memory banks** for maintaining project context across AI sessions

## 💡 Best Practices

### For Vibe Coding (Lab 1)
- Start with high-level goals
- Iterate based on output
- Be prepared to course-correct
- Track the number of iterations needed

### For Spec-Driven Development (Lab 2)
- Provide detailed specifications upfront
- Include design mockups or wireframes
- Specify technical requirements clearly
- Use Cline's PLAN mode before implementation

### For MCP Servers (Lab 3)
- Design clear, focused tool interfaces
- Handle errors gracefully
- Document your tools thoroughly
- Test with real AI assistant queries

### For PLAN Mode (Lab 4)
- Ask exploratory questions first
- Build comprehensive memory banks
- Update context as the project evolves
- Use resources efficiently

## 🔗 Resources

### Documentation
- [GitHub Copilot Docs](https://docs.github.com/en/copilot)
- [Cline Documentation](https://github.com/cline/cline)
- [MCP Protocol Specification](https://modelcontextprotocol.io/)
- [OpenWeatherMap API](https://openweathermap.org/api)

### Further Learning
- Context Engineering best practices
- SpecKit specification format
- Advanced MCP server patterns
- AI-assisted development workflows

## 🤝 Contributing

This workshop is designed to be modular and extensible. Contributions are welcome:

- Additional app options for Labs 1-2
- New MCP server examples
- Additional specifications
- Improvements to existing labs

---

**Ready to start?** Head to [Lab 1](docs/labs/lab01-vibe-code/) to begin your agentic programming journey!

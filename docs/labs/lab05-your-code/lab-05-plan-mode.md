# Lab 5: PLAN Mode and Memory Banks

## 🎯 Objective

Learn to use Copilot and Cline in PLAN mode for intelligent codebase exploration, and create memory banks/context stores for ongoing project understanding.

**Time:** 35 minutes

---

## Learning Goals

By the end of this lab, you will:
- ✅ Use PLAN mode effectively for exploration
- ✅ Ask informed questions about unfamiliar codebases
- ✅ Create and maintain memory banks
- ✅ Build context stores for project continuity
- ✅ Understand when to use PLAN vs. ACT mode

---

## What is PLAN Mode?

### PLAN vs. ACT Mode

| Mode | Purpose | Makes Changes? |
|------|---------|----------------|
| **PLAN** | Exploration, analysis, understanding | ❌ No |
| **ACT** | Implementation, execution | ✅ Yes |

### When to Use PLAN Mode

```
✅ USE PLAN MODE:
├── Exploring an unfamiliar codebase
├── Understanding architecture decisions
├── Investigating bugs before fixing
├── Planning a feature implementation
├── Reviewing code for patterns
└── Building mental models

❌ DON'T USE PLAN (use ACT):
├── Implementing features
├── Fixing known bugs
├── Refactoring code
├── Writing new files
└── Executing planned changes
```

---

## Part A: PLAN Mode Exploration (15 minutes)

### Setup

For this lab, you'll explore the Weather App from Labs 1 & 2. You can use either version, or use any codebase you're less familiar with.

### Step 1: Enable PLAN Mode

**In Cline:**
- Look for the mode toggle in the Cline panel
- Select "Plan" mode (not "Act" or "Auto")

**In Copilot:**
- Copilot Chat is naturally exploratory
- Be explicit: "Don't make changes, just analyze..."

### Step 2: Ask Exploratory Questions

Use these prompts to explore the Weather App:

#### Architecture Questions
```
Analyze the architecture of this weather app. What patterns are used? 
How is the code organized? What are the main components?
```

#### Data Flow Questions
```
Trace the data flow when a user searches for weather. 
What functions are called? How does data move through the app?
```

#### Quality Questions
```
Review this codebase for potential issues. Are there any bugs, 
security concerns, or code quality problems?
```

#### Improvement Questions
```
If I wanted to add unit tests to this codebase, what would be the 
best approach? Which functions are most testable?
```

### Step 3: Document What You Learn

Create a file called `ARCHITECTURE.md`:

```markdown
# Weather App Architecture Analysis

## Overview
[What Cline/Copilot explained about the overall structure]

## Key Components
[List the main components identified]

## Data Flow
[Document how data flows through the app]

## Patterns Used
[Design patterns identified]

## Potential Improvements
[Suggestions from the AI]
```

**📝 Fill this in based on your PLAN mode exploration:**

```markdown
# Weather App Architecture Analysis

## Overview


## Key Components
1. 
2. 
3. 

## Data Flow


## Patterns Used


## Potential Improvements
1. 
2. 
3. 
```

---

## Part B: Building a Memory Bank (15 minutes)

### What is a Memory Bank?

A **Memory Bank** is a structured collection of context files that help AI assistants understand your project across sessions.

```
.memory/
├── ARCHITECTURE.md      # System design overview
├── DECISIONS.md         # Why things are the way they are
├── CONVENTIONS.md       # Coding standards and patterns
├── GLOSSARY.md          # Project-specific terminology
└── CURRENT_FOCUS.md     # What you're working on now
```

### Step 1: Create the Memory Bank Structure

Create a `.memory/` folder in your project:

```bash
mkdir .memory
```

### Step 2: Create Core Memory Files

**`.memory/ARCHITECTURE.md`**
```markdown
# Project Architecture

## Overview
This is a weather application built with vanilla web technologies.

## Tech Stack
- HTML5 for structure
- CSS3 for styling (no frameworks)
- JavaScript (ES6+) for logic
- OpenWeatherMap API for data

## File Structure

weather-app/
├── index.html      # Single-page application structure
├── styles.css      # All styling including responsive design
├── app.js          # Application logic, API calls, state management
└── README.md       # Documentation


## Key Architectural Decisions
1. **No frameworks**: Keep it simple and educational
2. **Single HTML file**: All UI in one place
3. **CSS Variables**: Easy theming and consistency
4. **Module pattern in JS**: Organized without build tools

## Component Overview
- **Search Component**: Input + buttons for city/zip/geolocation
- **Weather Display**: Current conditions card
- **Forecast Component**: 5-day forecast cards
- **State Management**: Simple show/hide with CSS classes
```

**`.memory/DECISIONS.md`**
```markdown
# Architectural Decisions

## ADR-001: Vanilla JavaScript Over Framework
**Date**: [Date]
**Status**: Accepted

### Context
Need to build a weather app for educational purposes.

### Decision
Use vanilla JavaScript without React/Vue/Angular.

### Consequences
- ✅ Lower barrier to entry for learners
- ✅ No build tooling required
- ❌ More boilerplate for DOM manipulation
- ❌ Manual state management

---

## ADR-002: OpenWeatherMap API
**Date**: [Date]
**Status**: Accepted

### Context
Need a reliable weather data source with free tier.

### Decision
Use OpenWeatherMap API.

### Consequences
- ✅ Free tier sufficient for development
- ✅ Well-documented
- ❌ API key required
- ❌ Rate limits on free tier
```

**`.memory/CONVENTIONS.md`**
```markdown
# Coding Conventions

## JavaScript
- Use `const` by default, `let` when reassignment needed
- Async/await over raw promises
- Descriptive function names (verb + noun)
- JSDoc comments for public functions

## CSS
- Use CSS custom properties for theming
- BEM-like naming: `.component`, `.component-element`
- Mobile-first responsive design
- Use `rem` for typography, `px` for borders

## HTML
- Semantic elements (header, main, section, footer)
- ARIA labels for accessibility
- Data attributes for JS hooks

## Git
- Conventional commits: feat:, fix:, docs:, style:
- Branch naming: feature/, bugfix/, hotfix/
```

**`.memory/GLOSSARY.md`**
```markdown
# Project Glossary

## Terms

### Weather Data
- **Current Weather**: Real-time weather conditions
- **Forecast**: Predicted weather (3-hour intervals from API)
- **Feels Like**: Apparent temperature accounting for humidity/wind

### UI States
- **Initial State**: Welcome screen before any search
- **Loading State**: Spinner while fetching data
- **Error State**: Display when something fails
- **Weather State**: Showing weather results

### API
- **API Key**: Authentication token for OpenWeatherMap
- **Imperial Units**: Fahrenheit, mph, miles
- **Metric Units**: Celsius, km/h, kilometers
```

**`.memory/CURRENT_FOCUS.md`**
```markdown
# Current Focus

## Active Work
[What you're currently working on]

## Recent Changes
- [List recent changes]

## Known Issues
- [ ] [List known issues]

## Next Steps
1. [Next task]
2. [Following task]
```

### Step 3: Configure AI to Use Memory Bank

When starting a new session, reference your memory bank:

**Prompt Template:**
```
I'm working on the weather app project. Please read the context files 
in the .memory/ folder to understand the project before we begin.

Current focus: [What you're working on today]
```

Or add to your `.clinerules` file:
```
# Cline Rules

## Context Loading
Always read files in .memory/ at the start of a session to understand:
- Project architecture (ARCHITECTURE.md)
- Why decisions were made (DECISIONS.md)
- Coding standards (CONVENTIONS.md)
- Terminology (GLOSSARY.md)
- Current work (CURRENT_FOCUS.md)

## Behavior
- Follow conventions in CONVENTIONS.md
- Update CURRENT_FOCUS.md when starting new work
- Add new decisions to DECISIONS.md
- Add new terms to GLOSSARY.md
```

---

## Part C: Using Memory in Practice (5 minutes)

### Test Your Memory Bank

With your memory bank in place, try these prompts:

#### Context-Aware Question
```
Based on our architecture, what would be the best way to add a 
temperature unit toggle (F/C)?
```

#### Convention-Aware Request
```
Add a search history feature following our coding conventions.
```

#### Decision-Aware Discussion
```
We're considering adding React to this project. Given our ADR about 
vanilla JavaScript, what are the trade-offs?
```

### Observe the Difference

**Without Memory Bank:**
- AI might suggest approaches that don't fit your patterns
- May use different coding style
- Could contradict previous decisions

**With Memory Bank:**
- AI respects established patterns
- Maintains consistency
- Understands context without re-explaining

---

## 📊 Memory Bank Best Practices

### What to Include

| File | Content | Update Frequency |
|------|---------|------------------|
| ARCHITECTURE.md | System design, components | When structure changes |
| DECISIONS.md | ADRs, why not just what | Per significant decision |
| CONVENTIONS.md | Code style, patterns | When standards evolve |
| GLOSSARY.md | Domain terms | As terms are introduced |
| CURRENT_FOCUS.md | Active work | Every session |

### What NOT to Include

❌ Don't put in memory bank:
- Sensitive credentials
- Large code dumps
- Frequently changing details
- Information better in code comments

### Maintenance Tips

1. **Review weekly** - Keep memory bank accurate
2. **Prune outdated info** - Remove stale decisions
3. **Add as you go** - Document decisions when made
4. **Keep it concise** - AI reads this every session

---

## 🔑 Key Takeaways

### PLAN Mode Benefits

1. **Safe exploration** - No accidental changes
2. **Deep understanding** - Ask questions freely  
3. **Better plans** - Informed implementation
4. **Knowledge building** - Learn the codebase

### Memory Bank Benefits

1. **Session continuity** - AI remembers context
2. **Consistency** - Patterns are followed
3. **Onboarding** - New team members learn fast
4. **Decision tracking** - Know why things exist

### The Workflow

```
┌─────────────────────────────────────────────────────────────┐
│                                                              │
│  1. START SESSION                                            │
│     └── Load memory bank context                             │
│                                                              │
│  2. PLAN MODE                                                │
│     └── Explore, question, understand                        │
│                                                              │
│  3. UPDATE FOCUS                                             │
│     └── Document what you're working on                      │
│                                                              │
│  4. ACT MODE                                                 │
│     └── Implement with full context                          │
│                                                              │
│  5. END SESSION                                              │
│     └── Update memory bank with learnings                    │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 🚀 Advanced: Cline Rules File

For Cline users, create a `.clinerules` file in your project root:

```markdown
# Project: Weather App

## Context
This is an educational weather application demonstrating vanilla web development.
Always read .memory/ files at the start of conversations.

## Coding Standards
- Use ES6+ JavaScript features
- Follow existing patterns in the codebase
- Maintain the current file structure
- Use CSS variables for any new styling

## Behavior
- Ask clarifying questions for ambiguous requests
- Explain reasoning before making changes
- Suggest tests for new functionality
- Update documentation for new features

## Restrictions
- Do not add npm dependencies without discussion
- Do not change the fundamental architecture
- Do not modify API key handling
- Keep the app framework-free
```

---

## ✅ Completion Checklist

Before wrap-up:

- [ ] Used PLAN mode to explore a codebase
- [ ] Created a `.memory/` folder with context files
- [ ] Documented architecture and decisions
- [ ] Tested memory bank with context-aware prompts
- [ ] Understand PLAN vs. ACT mode differences

---

## 💭 Discussion Questions

1. How would you maintain a memory bank for a large team?
2. What other files would be useful in a memory bank?
3. How does this compare to traditional documentation?
4. When would PLAN mode slow you down?

---

## 📚 Resources

- [Cline Rules Documentation](https://github.com/cline/cline)
- [GitHub Copilot Best Practices](https://docs.github.com/en/copilot)
- [Architecture Decision Records](https://adr.github.io/)
- [Context Engineering Patterns](https://www.anthropic.com/research)

---

*Workshop Complete! Return to [Agenda](../../AGENDA.md) for wrap-up.*
